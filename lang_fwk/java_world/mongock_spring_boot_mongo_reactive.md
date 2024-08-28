

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
            <artifactId>mongodb-reactive-driver</artifactId>
            <version>5.2.4</version>
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
        enabled: true


## OrderServiceApplication.java


	@SpringBootApplication(scanBasePackages = "fr.company.example.orderservice")
	@EnableMongock
	public class OrderServiceApplication {
	
	  public static void main(String[] args) {
	    SpringApplication.run(SpringBootMongodbReactiveApplication.class, args);
	  }
	
	}


 ## src/main/java/fr/company/example/orderservice/migration/InitCollectionsChangeLog.java

	@ChangeUnit(id = "init-customer", order = "001", author = "bootify")
	public class InitCollectionsChangeLog {

 		private final ReactiveMongoTemplate template;

   		public InitCollectionsChangeLog(ReactiveMongoTemplate template) {
			this.template = template;
  		}
	
	    @BeforeExecution
	    public void beforeExecution(final MongoTemplate mongoTemplate) {
	        this.template.createCollection("customer", CollectionOptions.empty()
	                .validator(Validator.schema(MongoJsonSchema.builder()
	                .required("firstName", "lastName", "email")
	                .properties(
	                        JsonSchemaProperty.int64("id"),
	                        JsonSchemaProperty.string("firstName"),
	                        JsonSchemaProperty.string("lastName"),
	                        JsonSchemaProperty.string("email")).build())))
	                .subscribe();
	    }
	
	    // @RollbackBeforeExecution, @Execution, @RollbackExecution
	
	}

## Credits


Config old, but good example :

https://bootify.io/mongodb/mongock-in-spring-boot-maven.html


