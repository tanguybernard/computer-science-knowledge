# Spring

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

### Jour 2
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
### Jour 3
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
### Jour 4
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
