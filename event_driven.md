# Event Driven

## Message queue

Message Queue est l'échange utilisé par les microservices ou les systèmes distribués afin qu'ils puissent communiquer, ce qui permet à l'architecture d'évoluer horizontalement en fonction de la charge ou du nombre de messages en suspens qui attendent d'être consommés. 
Message queue utilise la file d'attente comme moyen d'échange et se compose d'un service de publication et de plusieurs services de consommation. 
Les messages sont placés dans la file d'attente en FIFO (First in First Out). Lorsque le message est consommé par l'un des consommateurs, il est retiré de la file d'attente ou de l'échange.

Exemple: Envoi de mail, on peut monter plusieurs seveur mail pour envoyer les messages, peut importe qui prends le message dans la queue.

## Pub/Sub

Un pub/sub c'est enfaite une multitude de message queue.


Exemple: Plusieurs services qui veulent etre notifié qu'un contrat pour un utilisateur a été crée, chacun sera interessé par tout ou partie du details de ce contract. 

Exemple contrat box internet, telphonie, chaines télévision en option, internet, netflix...
Chaque service voudra etre notifié si l'utilisateur possède un contrat et dans quel modalité, je souscris a une offre box avec netflix, quel abonnement netflix est choisi dedans HD, fullHD, 1 appreil, 4 appareils...

## Credits

https://www.youtube.com/watch?v=hl2BQIW343k&list=PLv7xGPH0RMUQC6eKGeEXO4PzvKdsU7z2j&index=39
