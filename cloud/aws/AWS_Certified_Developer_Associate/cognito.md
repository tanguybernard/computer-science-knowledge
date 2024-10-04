

Tricks :

Dans Cognito on ne peut pas filtrer sur les custom attributs.

Il faut utiliser la Query en cli mais avec le sdk (en octobre 2024) l'option n'est pas disponible.

Voici un exmple pour une valeur ADMIN (attention c'est un filtre sur toutes les valeurs de n'importe quel attribut (custom:role, given_name, phone_number...))

    aws cognito-idp list-users --user-pool-id <userPoolId> --query "Users[?contains(Attributes[].Value, 'ADMIN')]"
