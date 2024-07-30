# Spring


## rogrammation par aspects (AOP)

La programmation par aspects (AOP) est un paradigme de programmation qui vise à augmenter la modularité en permettant la séparation des préoccupations transversales.


Concepts Clés de l'AOP

- Aspect : Une classe qui modularise une préoccupation transversale. Un aspect contient des conseils (advices), des points de jonction (join points) et des pointcuts.

- Advice : Le code qui est exécuté à un certain point de l'exécution du programme. Il peut être exécuté avant, après ou autour d'un point de jonction spécifié.

- Join Point : Un point dans l'exécution du programme où un aspect peut être appliqué. Par exemple, l'appel d'une méthode ou l'accès à un attribut.

- Pointcut : Une expression qui sélectionne un ou plusieurs points de jonction où un advice doit être appliqué.

- Weaving : Le processus d'intégration des aspects dans le code principal du programme. Cela peut se faire à la compilation, au chargement de classe (load-time), ou à l'exécution (runtime).


Exemple :

Aspect

	import org.aspectj.lang.annotation.Aspect;
	import org.aspectj.lang.annotation.Before;
	import org.springframework.stereotype.Component;
	
	@Aspect
	@Component
	public class LoggingAspect {
	
	    @Before("execution(* com.example.service.*.*(..))")
	    public void logBeforeMethodExecution() {
	        System.out.println("Method execution logged before actual execution.");
	    }
	}

Code 

	package com.example.service;
	
	import org.springframework.stereotype.Service;
	
	@Service
	public class MyService {
	
	    public void performTask() {
	        System.out.println("Task performed.");
	    }
	}




Explication de l'Exemple

- Aspect : LoggingAspect est défini comme un aspect avec l'annotation @Aspect.
- Advice : La méthode logBeforeMethodExecution est un advice qui utilise l'annotation @Before pour spécifier qu'il doit être exécuté avant les méthodes correspondant au pointcut défini.
- Join Point : Les points de jonction sont toutes les méthodes dans le package com.example.service.
- Pointcut : execution(* com.example.service.*.*(..)) sélectionne toutes les méthodes dans le package com.example.service.

## Project example

https://github.com/spring-petclinic/spring-framework-petclinic

## Dynamic beans

__tl;dr__

- make sure you absolutely need it
- implement BeanFactoryPostProcessor
- create BeanDefinition
- add BeanDefinition to BeanDefinitionRegistry

source: https://blog.pchudzik.com/201705/dynamic-beans/


## Quizz

### 1
​
- Citez les 4 caractéristiques de Spring
	> open source, lightweight, DI container, Framework
- Qu’est-ce qu’un conteneur d’injection de dépendances?
	> Application context, instancie les beans et injecte leurs dépendances
- Quel est le scope par défaut de vos beans
	> Singleton
- Quelles sont les différentes façons de définir vos beans?
	> En java config : méthodes @Bean dans une classe annotée @Configuration; Par annotations : @ComponentScan + @Component sur les classes (ou stéréotypes). XML également possible mais pas vu
- Combien de profils peut-on activer simultanément?
	> Autant que l’on veut. Attention lorsqu’un profil est activé, les beans sans profils sont également disponibles.
- Citez toutes les annotations dont vous vous souvenez
	> @Component et les stéréotypes @Service, @Repository, @Controller, @Configuration...
​
### 2
​
- Quelles sont les problématiques que l’AOP essaie de résoudre?
	> Cross cutting concerns (problématiques transverses). Sans ça, on voit apparaitre du code tangling (code emêlé, couplé) et du code scattering (code dupliqué, éparpillé)
- Quels sont les différents concepts utilisés dans l’AOP ? (vocabulaire)
	> Joinpoint, Pointcut, Advice, Aspect, Weaving
- Citez les 5 types d’Advices disponibles.
	> @Before, @After, @AfterThrowing, @AfterReturning, @Around
- Quelle est l’annotation à utiliser pour configurer un application contexte de test avec JUnit ?
	> @SpringJunitConfig(MaClasseDeConfig.class) (ou @ExtendWith(SpringExtension.class) + @ContextConfiguration(MaClasseDeConfig.class))
- Quels sont les problèmes de l’api JDBC ?
	> Beaucoup de boilerplate, checked exception, ouverture et fermeture de la connexion à gérer.
- Quelles sont les caractéristiques d’une transaction?
	> ACID : Atomic, Consistent, Isolated, Durable
​
### 3
​
- Quelles sont les fonctionnalités majeures de Spring Boot?
	> Dependency management, Auto configuration, packaging, test integration
- Sous quelles conditions l’autoconfiguration peut-elle créer des beans?
	> @ConditionalOnMissingBean, @Profil, @ConditionalOnProperty, @ConditionalOnMissingClass ...
- Comment personnaliser la configuration automatique?
	> On peut définir notre propre bean, utiliser des properties, exclure des classes d’autoconfiguration, modifier les dépendances
- Quelles sont les étapes pour mettre en place Spring Data?
	> ajouter spring-boot-starter-data-jpa, annoter nos entities (@Entity + @Id au minimum), définir nos repositories
- Quel mécanisme permet de fournir une implémentation au runtime des interfaces Repository?
	> les Instant Repository de Spring Data, et c’est les BeanPostProcessor qui vont les implémenter dans des proxy.
- Quel composant Spring permet de déserialiser le body de la requête HTTP et de sérialiser la réponse?
	> Les Message Converter qui sont autoconfigurés par Spring Boot. Ils sont utilisés pour les @RequestBody, les @ResponseBody, et pour tout retour des méthodes d’une classe annotée @RestController
