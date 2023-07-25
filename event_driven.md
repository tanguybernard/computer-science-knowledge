# Event Driven

## Message queue

Message Queue est l'échange utilisé par les microservices ou les systèmes distribués afin qu'ils puissent communiquer, ce qui permet à l'architecture d'évoluer horizontalement en fonction de la charge ou du nombre de messages en suspens qui attendent d'être consommés. 
Message queue utilise la file d'attente comme moyen d'échange et se compose d'un service de publication et de plusieurs services de consommation. 
Les messages sont placés dans la file d'attente en FIFO (First in First Out). Lorsque le message est consommé par l'un des consommateurs, il est retiré de la file d'attente ou de l'échange.
