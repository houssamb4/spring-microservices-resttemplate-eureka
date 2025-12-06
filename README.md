# TP 20 : Architecture Microservices avec Spring Boot, Eureka, RestTemplate et Gateway

## Présentation

Ce projet illustre une architecture microservices basée sur Spring Boot, avec les composants suivants :
- **Eureka Server** : Service de découverte permettant aux microservices de s’enregistrer et de se découvrir dynamiquement.
- **Gateway** : Passerelle API centralisant l’accès aux microservices et gérant le routage dynamique.
- **Service Client** : Microservice gérant les clients (CRUD).
- **Service Voiture** : Microservice gérant les voitures, avec association à un client et communication inter-service via RestTemplate.

## Structure du projet

```
eureka-server/      # Serveur Eureka (discovery)
gateway/            # Passerelle API (Spring Cloud Gateway)
client-service/     # Microservice de gestion des clients
service-voiture/    # Microservice de gestion des voitures
```

## Fonctionnalités principales

- **Découverte de services** : Les microservices s’enregistrent auprès d’Eureka et sont accessibles via la Gateway.
- **Communication inter-services** : Utilisation de RestTemplate pour récupérer les informations d’un client depuis le service voiture.
- **Base de données indépendante** : Chaque microservice possède sa propre base MySQL.
- **Endpoints REST** :
  - `client-service` : `/api/client` (GET, POST, GET/{id})
  - `service-voiture` : `/api/car` (GET, POST, PUT/{id}, DELETE/{id})
- **Configuration centralisée** : Utilisation de fichiers `application.yml` pour chaque service.

## Démarrage rapide

1. **Lancer Eureka Server**  
   ```
   cd eureka-server
   ./mvnw spring-boot:run
   ```
   Accès à la console Eureka : [http://localhost:8761](http://localhost:8761)

2. **Lancer Gateway**  
   ```
   cd gateway
   ./mvnw spring-boot:run
   ```

3. **Lancer les microservices**  
   ```
   cd client-service
   ./mvnw spring-boot:run

   cd service-voiture
   ./mvnw spring-boot:run
   ```

4. **Accéder aux endpoints via la Gateway**  
   Exemple :  
   - [http://localhost:8888/service-client/api/client](http://localhost:8888/service-client/api/client)
   <img width="529" height="638" alt="Image" src="https://github.com/user-attachments/assets/c043abc1-3baf-4b50-9375-f5df634d9ad9" />
   - [http://localhost:8888/service-voiture/api/car](http://localhost:8888/service-voiture/api/car)
   <img width="633" height="916" alt="Image" src="https://github.com/user-attachments/assets/1da6d1d0-ff6b-43b9-8b75-07be7a20c59f" />

## Extensions possibles

- Sécurisation des API (Spring Security, OAuth2)
- Résilience (Circuit Breaker avec Resilience4j)
- Monitoring (Spring Boot Actuator, Prometheus, Grafana)
- Traçabilité (Spring Cloud Sleuth, Zipkin)
- Documentation API (Swagger/OpenAPI)
- Configuration centralisée (Spring Cloud Config)

## Bonnes pratiques

- Chaque microservice a sa propre base de données.
- La communication se fait via des API REST et la découverte dynamique.
- La Gateway centralise l’accès et le routage.
- Les configurations sont externalisées.
- La gestion des erreurs et la résilience sont essentielles.

---
