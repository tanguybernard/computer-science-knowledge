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




