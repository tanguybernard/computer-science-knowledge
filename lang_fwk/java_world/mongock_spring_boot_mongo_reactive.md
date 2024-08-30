

## pom.xml

	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.2.2</version>
		<relativePath />
	</parent>
    <dependencies>
	<dependency>
	    <groupId>org.springframework.boot</groupId>
	    <artifactId>spring-boot-starter-data-mongodb-reactive</artifactId>
	    <version>3.2.3</version>
	</dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-mongodb</artifactId>
            <version>3.2.3</version>
        </dependency>
        <dependency>
            <groupId>io.mongock</groupId>
            <artifactId>mongodb-springdata-v3</artifactId>
            <version>5.2.4</version>
        </dependency>
        <dependency>
            <groupId>io.mongock</groupId>
            <artifactId>mongodb-springdata-v4-driver</artifactId>
            <version>5.2.4</version>
        </dependency>
    </dependencies>


## application.yml

    mongock:
        migration-scan-package: fr.company.example.orderservice.migration


## OrderServiceApplication.java

 ```java
@SpringBootApplication(scanBasePackages = "fr.company.example.orderservice")
@EnableMongock
public class OrderServiceApplication {

  public static void main(String[] args) {
    SpringApplication.run(SpringBootMongodbReactiveApplication.class, args);
  }

}
 ```

 ### Migration 1 pour créer une collection et le schéma de validation

 ```java
//src/main/java/fr/company/example/orderservice/migration/Migration1.java


package fr.edf.tipienergy.orderservice.migration;

import io.mongock.api.annotations.*;
import org.springframework.data.mongodb.core.CollectionOptions;
import org.springframework.data.mongodb.core.ReactiveMongoTemplate;
import org.springframework.data.mongodb.core.schema.JsonSchemaObject;
import org.springframework.data.mongodb.core.schema.JsonSchemaProperty;
import org.springframework.data.mongodb.core.schema.MongoJsonSchema;
import org.springframework.data.mongodb.core.validation.Validator;
import reactor.core.publisher.Mono;


@ChangeUnit(id = "init-orders", order = "001", author = "TB00E36L")
public class Migration20240829 {


    private final ReactiveMongoTemplate template;

    private Boolean orderCollectionExist;

    public Migration20240829(ReactiveMongoTemplate template) {
	this.template = template;
    }


    @BeforeExecution
    public void beforeExecution() {
	orderCollectionExist = template.collectionExists("orders").block();

    }


    @RollbackBeforeExecution
    public void rollbackBeforeExecution() {

    }

    @Execution
    public void execution() {
	if(!orderCollectionExist){
	    this.createCollectionIfNotExists("orders").subscribe();
	}
    }

    @RollbackExecution
    public void rollbackExecution() {

    }



    public Mono<Void> createCollectionIfNotExists(String collectionName) {

	var schema = createSchema();
	CollectionOptions options = CollectionOptions.empty()
		.validator(Validator.schema(schema));

	return template.createCollection(
				collectionName,
				options).then();

    }

    public MongoJsonSchema createSchema() {
	return MongoJsonSchema.builder()
		.required("num")
		.properties(
			JsonSchemaProperty.string("num"),
			JsonSchemaProperty.array("offers").items(
				JsonSchemaObject.object()
					.properties(
						JsonSchemaProperty.string("type"),
						JsonSchemaProperty.int32("powerplantId"),
						JsonSchemaProperty.string("powerplantName"),
						JsonSchemaProperty.int32("includingTaxPriceByTiwatt"),
						JsonSchemaProperty.array("tiwatts")
			)),
			JsonSchemaProperty.object("delivery").properties(
				JsonSchemaProperty.string("firstName"),
				JsonSchemaProperty.string("lastname"),
				JsonSchemaProperty.string("address"),
				JsonSchemaProperty.string("additionalAddress"),
				JsonSchemaProperty.string("city"),
				JsonSchemaProperty.string("zipcode"),
				JsonSchemaProperty.string("iban")
			),
			JsonSchemaProperty.date("creationDate"),
			JsonSchemaProperty.object("customer"),
			JsonSchemaProperty.string("status")
		)
		.build();
    }

}
 ```

### Migration2  Pour mettre a jour le schéma de validation

 ```java
package fr.edf.tipienergy.orderservice.migration;

import io.mongock.api.annotations.*;
import org.bson.Document;
import org.springframework.data.mongodb.core.CollectionOptions;
import org.springframework.data.mongodb.core.ReactiveMongoTemplate;
import org.springframework.data.mongodb.core.schema.JsonSchemaObject;
import org.springframework.data.mongodb.core.schema.JsonSchemaProperty;
import org.springframework.data.mongodb.core.schema.MongoJsonSchema;
import org.springframework.data.mongodb.core.validation.Validator;
import reactor.core.publisher.Mono;


@ChangeUnit(id = "update", order = "002", author = "TB00E36L")
public class Migration20240830 {


    private final ReactiveMongoTemplate template;

    private Boolean orderCollectionExist;

    public Migration20240830(ReactiveMongoTemplate template) {
	this.template = template;
    }


    @BeforeExecution
    public void beforeExecution() {
    }


    @RollbackBeforeExecution
    public void rollbackBeforeExecution() {
    }

    @Execution
    public void execution() {

	this.updateCollectionSchema("orders").block();
	System.out.println("FINISH");
    }

    @RollbackExecution
    public void rollbackExecution() {
    }

    public Mono<Void> updateCollectionSchema(String collectionName) {
	var schema = createUpdatedSchema();
	CollectionOptions options = CollectionOptions.empty()
		.validator(Validator.schema(schema));

	return template.collectionExists(collectionName)
		.flatMap(exists -> {
		    if (exists) {
			var command =
				Document.parse("{ collMod: '" + collectionName + "', validator: " + schema.toDocument().toJson() + " }");

			return  Mono.from(template.getMongoDatabase().block().runCommand(command)).then();
		    } else {
			return template.createCollection(collectionName, options).then();
		    }
		});
    }

    public MongoJsonSchema createUpdatedSchema() {
	return MongoJsonSchema.builder()
		.required("num")
		.properties(
			JsonSchemaProperty.string("num"),
			JsonSchemaProperty.array("offers").items(
				JsonSchemaObject.object()
					.properties(
						JsonSchemaProperty.string("type"),
						JsonSchemaProperty.int32("powerplantId"),
						JsonSchemaProperty.string("powerplantName"),
						JsonSchemaProperty.int32("includingTaxPriceByTiwatt"),
						JsonSchemaProperty.array("tiwatts")
					)),
			JsonSchemaProperty.object("delivery").properties(
				JsonSchemaProperty.string("firstName"),
				JsonSchemaProperty.string("lastname"),
				JsonSchemaProperty.string("address"),
				JsonSchemaProperty.string("additionalAddress"),
				JsonSchemaProperty.string("city"),
				JsonSchemaProperty.string("zipcode"),
				JsonSchemaProperty.string("iban")
			),
			JsonSchemaProperty.date("creationDate"),
			JsonSchemaProperty.object("customer"),
			JsonSchemaProperty.string("status"),
			// Nouveaux champs ajoutés ici
			JsonSchemaProperty.string("newField1"),
			JsonSchemaProperty.object("newField2").properties(
				JsonSchemaProperty.string("subField1"),
				JsonSchemaProperty.int32("subField2")
			)
		)
		.build();
    }



}
 ```


## Credits


Config old, but good example :

https://bootify.io/mongodb/mongock-in-spring-boot-maven.html


