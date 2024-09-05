# SES


## Avant d'utiliser la CLI si on passe par VPN

    export http_proxy=http://vip-users.proxy.company.fr:3131/
    export https_proxy=http://vip-users.proxy.company.fr:3131/

    export AWS_PROFILE=defaut


## Commandes

### List templates

     aws ses list-templates --profile defaut


### Get template

    aws ses get-template --template-name send_contact

### Create

    aws ses create-template --cli-input-json file://mytemplate.json


### Update (Le json doit etre encodé en windows-1252 - ANSI )

aws ses update-template --cli-input-json file://path/to/update_template.json


    {
        "Template": {
            "TemplateName": "send_contact",
            "SubjectPart": "[Contact] Vous avez reçu un nouveau message",
            "TextPart": "Une nouvelle demande de contact par un {{type}}!\r\nNom : {{lastname}}\r\nPrénom : {{firstname}}\r\nEmail : {{email}}\r\nTéléphone : {{phone}}\r\nVille : {{city}} ({{zipcode}})\r\nMessage : {{message}}",
            "HtmlPart": "<h1>Une nouvelle demande de contact par un {{type}}!</h1><p>Nom : {{lastname}}.</p><p>Prénom : {{firstname}}.</p><p>Email : {{email}}.</p><p>Téléphone : {{phone}}.</p><p>Ville : {{city}} ({{zipcode}}).</p><p>Message : {{message}}.</p>"
        }
    }

### Condition

    {
        "Template": {
            "TemplateName": "send_contact",
            "SubjectPart": "[Contact] Vous avez reçu un nouveau message",
            "TextPart": "Une nouvelle demande de contact par un {{type}}!\r\nNom : {{lastname}}\r\nPrénom : {{firstname}}\r\nEmail : {{email}}\r\nT&eacute;léphone : {{phone}}\r\nVille : {{city}} ({{zipcode}})\r\nNewsletter : {{#if isAcceptedNewsletter}}Oui{{else}}Non{{/if}}\r\nMessage : {{message}}",
            "HtmlPart": "<h1>Une nouvelle demande de contact par un {{type}}!</h1><p>Nom : {{lastname}}.</p><p>Prénom : {{firstname}}.</p><p>Email : {{email}}.</p><p>T&eacute;l&eacute;phone : {{phone}}.</p><p>Ville : {{city}} ({{zipcode}}).</p><p>Newsletter :{{#if isAcceptedNewsletter}}Oui{{else}}Non{{/if}}</p><p>Message : {{message}}.</p>"
        }
    }



### Envoi  (Source il faut utiliser @ une adresse qui est domaine par exmple no-replay@compagnydomaine.fr)

    aws ses send-templated-email --cli-input-json file://myemail.json

myemail.json

    {
      "Source": "no-replay@emaildomain.fr",
      "Template": "send_contact",
      "Destination": {
        "ToAddresses": [ "tanguy@company.fr"
        ]
      },
      "ConfigurationSetName": "",
      "TemplateData": "{ \"firstname\":\"John\", \"lastname\": \"Doe\", \"phone\": \"010203\", \"city\": \"Nanterre\",\"zipcode\": \"92000\", \"isAcceptedNewsletter\": true, \"email\": \"test\", \"type\": \"PART\", \"message\": \"Ceci est un test !!!\" }"
    }
