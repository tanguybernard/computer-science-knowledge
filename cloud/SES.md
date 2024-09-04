# SES


## Avant d'utiliser la CLI si on passe par VPN

    export http_proxy=http://vip-users.proxy.company.fr:3131/
    export https_proxy=http://vip-users.proxy.company.fr:3131/

    export AWS_PROFILE=defaut


## Commandes

List templates

     aws ses list-templates --profile defaut


Get template

    aws ses get-template --template-name send_contact



Update 

aws ses update-template --cli-input-json file://path/to/update_template.json


    {
        "Template": {
            "TemplateName": "send_contact",
            "SubjectPart": "[Contact] Vous avez reçu un nouveau message",
            "TextPart": "Une nouvelle demande de contact par un {{type}}!\r\nNom : {{lastname}}\r\nPrénom : {{firstname}}\r\nEmail : {{email}}\r\nTéléphone : {{phone}}\r\nVille : {{city}} ({{zipcode}})\r\nMessage : {{message}}",
            "HtmlPart": "<h1>Une nouvelle demande de contact par un {{type}}!</h1><p>Nom : {{lastname}}.</p><p>Prénom : {{firstname}}.</p><p>Email : {{email}}.</p><p>Téléphone : {{phone}}.</p><p>Ville : {{city}} ({{zipcode}}).</p><p>Message : {{message}}.</p>"
        }
    }



    {
        "Template": {
            "TemplateName": "send_contact",
            "SubjectPart": "[Contact] Vous avez reçu un nouveau message",
            "TextPart": "Une nouvelle demande de contact par un {{type}}!\r\nNom : {{lastname}}\r\nPrénom : {{firstname}}\r\nEmail : {{email}}\r\nTéléphone : {{phone}}\r\nVille : {{city}} ({{zipcode}})\r\nMessage : {{message}}",
            "HtmlPart": "<h1>Une nouvelle demande de contact par un {{type}}!</h1><p>Nom : {{lastname}}.</p>
            <p>Prénom : {{firstname}}.</p><p>Email : {{email}}.</p><p>Téléphone : {{phone}}.</p><p>Ville : {{city}} ({{zipcode}}).</p>
            <p>Newsletter :{{#if isAcceptedNewsletter}}Oui{{else}}Non{{/if}}</p>
            <p>Message : {{message}}.</p>"
        }
    }
