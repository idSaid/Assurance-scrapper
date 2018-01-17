# Assurance-scrapper
Application Spring cloud (architecture en micro-services) qui check pour un utilisateur donné si il a eu un remboursement (en scrappant les sites d'assurances auxquelles il est affilié) et lui envoi un mail dès qu'elle en trouve un.

#Architecture de l’application
Notre application distribuée est articulée autour de micro-services réalisés grâce
au framework Spring Boot :
● config-service
    Centralise les différentes configurations des autres micro-services.
● eureka-service
    Service d’enregistrement sur lequel s’enregistrent les micros-services pour publier leurs services.
● proxy-service
    Point d’entrée unique pour le client ; c’est un micro-service qui permet d’acheminer les requêtes clients vers le micro-service cible et dispatche les requêtes sur les différentes instances de ce dernier.
    Le client ne doit pas se soucier des différentes adresses et ports sur lesquels sont lancés les micro-services.
● user-manager-service
    Est chargé de la gestion des utilisateurs, lié à à une base de données postgres.
● scrapper-service
    Dédié au scrapping des différents sites internet. Lié à une autre base de données postgres.
● mail-service
    Permet d’envoyer des mails aux différents clients ayant reçus des remboursements.
● client-AngularJS
    Client web permettant au client d’interagir avec l’application.

=========================================================

#Pour lancer l'application:

Lancer les micro-service Spring-boot
	_ config-service
	_ eureka-service
	_ proxy-service
	_ user-manager-service
	_ scrapper-service
	_ mail-sender-service

Lancer le client-angular sur un serveur php ou autres.


Pour des fins de tests nous avons fixé les ports des services.
Les fichiers properties des différents micro-services sont regroupés dans config-service-properties.

pour pouvoir lancer plusieurs instances du même service on doit 
	_ commenter le port dans l'application.properties
	_ lancer les instances sur des ports différents
(le proxy-service assure l'acheminement des requêtes utilisateurs)

#requirements:
RabbitMQ doit être lancer pour permettre la communication asynchrone entre les différents micro-services.
