

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
        migration-scan-package: fr.edf.tipienergy.orderservice.migration
        enabled: true


        


