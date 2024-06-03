# Serverless Framework


https://www.freecodecamp.org/news/how-to-deploy-aws-lambda-with-serverless/#what-is-serverless-framework

Serverless Framework est un outil puissant qui simplifie le déploiement et la gestion des applications sans serveur sur différents fournisseurs de cloud, notamment Amazon Web Services (AWS). 
Serverless Framework permet de déployer une simple fonction Python sur AWS Lambda, l'exposer via API Gateway et la surveiller à l'aide d'AWS CloudWatch.


## Comparaison

https://lumigo.io/aws-lambda-deployment/

Serverless

- beaucoup de contrôle sur le modèle CloudFormation
- plusieurs plugins (offline, dynamoDb...)
- supporte avec des plugins d'autres providers commme: Azure, GCP, IBM, CloudFlare...
- execution de lambda local

Serverless Application Model (SAM)

- cadre de déploiement officiel d'AWS
- construit au-dessus de CloudFormation (commme ServerlessFramework)
- execution de lambda local

Terraform

- un moyen de décrire et de créer votre infrastructure
- pas de support intégré pour empaqueter votre artefact de déploiement, ni pour exécuter des fonctions localement.


AWS Chalice (python), Zappa


https://lumigo.io/wp-content/uploads/2019/04/pasted-image-0-6.png
