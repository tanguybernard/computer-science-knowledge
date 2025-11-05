# BDD

**A déplacer dans une section à part.**


Spécification :

En tant qu'employé je veux pouvoir faire une demande de congé afin d'obtenir la validation de mon manager avant de partir.

Détails de spécification :

- L'employé saisi une date de début et de fin
- Il doit choisir un type de congé (CP, RTT, sans solde...)
- Le solde de congé doit etre positif
- La demande passe en attente de validation aupres du manager

Critères d'acceptation

Scénario 1 : Demande valide

GIVEN (Soit) un employé avec un solde de congé suffisant  
WHEN (Quand) il saisit une demande du 10 au 15 aout en "congé payé"  
THEN (Alors) la demande est enregistrée  
AND (Et) son statut est "en attente de validation"  
AND (Et) son solde est provisoirement diminué de 6 jours  

Scénario 2 : Solde insuffisant

GIVEN un employé avec un solde de 0 jours  
WHEN il saisit une demande du 10 au 15 aout en "congé payé"  
THEN la demande n'est pas enregistré
AND un message indique: "Pas de jours disponibles"






Critères d'acceptances :

