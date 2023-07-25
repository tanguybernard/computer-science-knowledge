# Event Driven

## Message queue

Message Queue est l'échange utilisé par les microservices ou les systèmes distribués afin qu'ils puissent communiquer, ce qui permet à l'architecture d'évoluer horizontalement en fonction de la charge ou du nombre de messages en suspens qui attendent d'être consommés. 
Message queue utilise la file d'attente comme moyen d'échange et se compose d'un service de publication et de plusieurs services de consommation. 
Les messages sont placés dans la file d'attente en FIFO (First in First Out). Lorsque le message est consommé par l'un des consommateurs, il est retiré de la file d'attente ou de l'échange.

Exemple: Envoi de mail, on peut monter plusieurs seveur mail pour envoyer les messages, peut importe qui prends le message dans la queue.

## Pub/Sub


L'architecture Pub-Sub est utilisée lorsque l'on veut quelque chose comme une diffusion. L'échange Pub-Sub peut consister en plusieurs services de production et plusieurs services de consommation. L'échange ou le courtier (broker) en messages garantit qu'au moins une copie de chaque message publié par le editeur est reçue par chaque abonné. En d'autres termes, dans l'architecture pub-sub, chaque message envoyé par l'éditeur est délivré à chaque abonné, abonné à un topic spécifique. Ainsi, contrairement à la file d'attente des messages (message queue), dans Pub-Sub, chaque abonné dispose de sa propre file d'attente, alors que dans la file d'attente des messages, tous les consommateurs partagent la même file d'attente.

Un pub/sub c'est enfaite une multitude de message queue.

Lorsque l'éditeur envoie un message à un thème, celui-ci le diffuse aux abonnés. Chaque abonné est lié à la file d'attente, de sorte que chaque file d'attente dispose d'un service d'écoute (ou abonné) qui attend le message.



Exemple: Plusieurs services qui veulent etre notifié qu'un contrat pour un utilisateur a été crée, chacun sera interessé par tout ou partie du details de ce contract. 

Exemple contrat box internet, telphonie, chaines télévision en option, internet, netflix...
Chaque service voudra etre notifié si l'utilisateur possède un contrat et dans quel modalité, je souscris a une offre box avec netflix, quel abonnement netflix est choisi dedans HD, fullHD, 1 appreil, 4 appareils...

## Credits

https://www.youtube.com/watch?v=hl2BQIW343k&list=PLv7xGPH0RMUQC6eKGeEXO4PzvKdsU7z2j&index=39

https://getkt.com/2023/02/22/message-queue-vs-pub-sub/
