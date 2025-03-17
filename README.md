# Mise en place d'une Piste d'Audit pour le Framework de Log

## 1. Introduction
La mise en place d’une piste d’audit est essentielle pour assurer la traçabilité des événements, faciliter l’analyse des incidents et répondre aux exigences de conformité (RGPD, CATS). Ce document détaille la mise en œuvre d’un système de journalisation centralisée.

## 2. Objectifs de la Piste d'Audit
- **Traçabilité des actions** : Enregistrement détaillé des événements et des interactions des utilisateurs avec le système. *(Permet de suivre précisément l’activité des applications et des utilisateurs.)*
- **Détection des anomalies** : Identification rapide des erreurs et incidents. *(Les logs aident à surveiller les performances, la fréquence des sollicitations et à identifier les problèmes.)*
- **Conformité** : Respect des obligations légales et des politiques de sécurité. *(Les logs doivent être conformes aux exigences de sécurité et respecter la politique RGPD.)*
- **Analyse et amélioration continue** : Exploitation des logs pour optimiser les performances et la sécurité. *(Grâce à l’agrégation, la corrélation et la visualisation des logs, les équipes peuvent détecter et résoudre les problèmes plus efficacement.)*

## 3. Collecte et Normalisation des Logs
### 3.1. Collecte Centralisée
- Mise en place d’un **framework de log** capable de collecter les logs provenant de différentes sources : applications, serveurs, systèmes de sécurité et équipements réseau. *(Les logs doivent être normalisés et collectés depuis plusieurs sources comme les applications, bases de données, serveurs et équipements réseau.)*
- Transmission des logs vers une solution centralisée comme **ELISA**. *(ELISA centralise les logs, mais une alternative est envisagée.)*
- Possibilité de faire évoluer la solution vers d’autres outils si nécessaire (ELK, autres SIEM). *(Actuellement, il n’est pas possible d’avoir un dashboard consolidé des namespaces dans ELISA, ce qui motive l’étude d’autres solutions.)*

### 3.2. Normalisation des Logs
- **Cohérence** : Uniformisation du format des logs pour une meilleure lisibilité et interopérabilité. *(Assurer que les informations sont enregistrées de manière homogène, quel que soit le composant ou service qui les génère.)*
- **Facilité d’analyse** : Structuration des logs pour permettre une recherche rapide et efficace. *(Les logs normalisés permettent une extraction efficace des informations et facilitent l’analyse des anomalies.)*
- **Interopérabilité** : Compatibilité avec des outils de supervision, gestion des incidents et sécurité. *(Les logs doivent être intégrés facilement avec d’autres systèmes pour une vision complète de l’infrastructure.)*
- **Identification des utilisateurs** : Transmission du matricule utilisateur et d’un **ID de corrélation** pour suivre les transactions. *(L’ID de corrélation doit être au niveau de la transaction et ne doit pas être confondu avec l’ID de session utilisateur.)*
- **Horodatage unique** : Synchronisation des horloges pour aligner les timestamps des événements enregistrés. *(Tous les logs doivent être basés sur une heure de référence unique pour faciliter l’analyse.)*

## 4. Activation Dynamique des Niveaux de Logs
- Modification du niveau de log **sans redémarrage** de l’application. *(Permet d’améliorer la flexibilité et la réactivité du système en cas de besoin.)*
- Interface utilisateur ou API permettant d’ajuster le niveau de granularité des logs. *(Une API ou une interface doit être disponible pour modifier dynamiquement le niveau de log.)*
- Application immédiate des modifications pour une meilleure réactivité en cas d’incident. *(Les changements doivent être effectifs sans nécessiter d’interruption du service.)*

## 5. Niveaux de Logs Définis
- **Fatal** : Erreur critique entraînant l’arrêt de l’application. *(Utilisé pour signaler des incidents majeurs nécessitant une intervention immédiate.)*
- **Error** : Erreur empêchant le bon fonctionnement d’une partie du système. *(Ne bloque pas nécessairement l’application mais requiert une attention.)*
- **Warning** : Problème potentiel nécessitant une attention particulière. *(Indique une anomalie qui pourrait affecter le fonctionnement normal.)*
- **Information** : Journaux informatifs sur l’activité normale. *(Utilisés pour suivre le fonctionnement de l’application.)*
- **Debug** : Détails techniques utiles au débogage. *(Activé uniquement dans les environnements de développement pour identifier et résoudre les problèmes.)*

## 6. Analyse et Alerting
- **Analyse des logs** via un outil unique dédié à la supervision et à l’exploitation. *(Les utilisateurs doivent pouvoir consulter les logs à partir d’une interface dédiée.)*
- **Création d’alertes** en fonction des erreurs critiques et des anomalies détectées. *(Le système doit pouvoir générer des alertes en cas d’anomalies détectées.)*
- **Visualisation et agrégation des logs** pour faciliter l’identification des problèmes. *(L’outil de restitution doit permettre la recherche, l’agrégation et la corrélation des logs.)*
- **Rapports et indicateurs clés** pour le suivi des performances et de la sécurité. *(Permet d’identifier les périodes de forte sollicitation et les erreurs récurrentes.)*

## 7. Sécurité et Conformité
- **Chiffrement et Sécurisation** : Les logs ne doivent pas transiter en clair et doivent être stockés de manière sécurisée. *(Les logs ne doivent pas contenir d’informations sensibles en clair et leur stockage doit être sécurisé.)*
- **Contrôle des accès** : Seules les personnes habilitées peuvent consulter les logs selon des règles précises (par application, environnement, etc.). *(Les habilitations doivent être gérées selon un modèle strict.)*
- **Anonymisation** : Possibilité de remplacer certaines valeurs sensibles par des données hachées. *(Les données stockées doivent être anonymisées pour respecter la réglementation RGPD.)*
- **Purge des logs** : Conservation des logs selon les normes définies (ex. 5 ans pour les logs d’accès, durée glissante pour les logs applicatifs). *(Les logs doivent être purgés de façon automatique pour assurer la conformité.)*

## 8. Exigences Techniques
- Support d’un **système d’identification unique** pour les événements. *(Chaque log doit contenir un identifiant de corrélation unique.)*
- Intégration avec les outils existants pour assurer une compatibilité et une interopérabilité optimale. *(Le framework doit pouvoir s’intégrer avec les outils d’analyse de logs comme ELISA.)*
- Mise en place d’une **solution évolutive**, incluant des mises à jour régulières et des améliorations continues. *(Le support technique doit garantir des mises à jour fréquentes et des corrections de sécurité.)*

## 9. Conclusion
Cette piste d’audit garantit un suivi détaillé des événements pour une meilleure gestion des incidents et une conformité renforcée. Sa mise en œuvre repose sur un cadre normalisé, une collecte centralisée et un système de supervision efficace. *(Une gestion centralisée des logs et une normalisation efficace permettent une exploitation optimale des informations collectées.)*

# TestingDotNetCore
TestingDotNetCore
# Améliorations et Ajouts pour SecuLogger

## 1. Introduction
Le `SecuLogger` a été mis en place pour gérer la piste d’audit dans le cadre du projet. Cependant, plusieurs éléments sont actuellement manquants ou nécessitent des améliorations pour être alignés avec l’expression du besoin du client. Cette documentation liste les **écarts**, les **améliorations nécessaires** et les **ajouts** à réaliser.

## 2. Écarts avec l'Expression du Besoin
### 2.1. Manque de Normalisation des Logs
- **Problème** : Les logs générés ne respectent pas encore un format normalisé.
- **Action nécessaire** : Ajouter un **formatter de logs** pour garantir une structure uniforme des événements (ex : JSON structuré avec champs obligatoires : timestamp, userID, action, statut, etc.).

### 2.2. Manque de Gestion des Niveaux de Sévérité
- **Problème** : Actuellement, `SecuLogger` implémente uniquement des méthodes `LogDebug`, `LogError`, `LogWarning`, mais **les niveaux de logs ne sont pas bien différenciés**.
- **Action nécessaire** : Ajouter des méthodes et une gestion des **niveaux critiques** en respectant la nomenclature :
  - `Fatal` : Crash de l'application.
  - `Error` : Échec d'une opération essentielle.
  - `Warning` : Problème non bloquant.
  - `Info` : Suivi d'exécution normal.
  - `Debug` : Informations techniques.
  - `Trace` : Détails bas niveau pour diagnostic.

### 2.3. Absence de Gestion des Identifiants d'Utilisateurs
- **Problème** : L'identifiant de session (`UserSessionId`) est loggé, mais **il manque un identifiant de corrélation** permettant de suivre une action de bout en bout.
- **Action nécessaire** :
  - Ajouter un **ID de transaction** unique par requête pour relier les événements entre eux.
  - Injecter cet ID automatiquement dans chaque log généré.

### 2.4. Sécurisation des Logs
- **Problème** : Certains logs pourraient contenir des données sensibles non anonymisées.
- **Action nécessaire** :
  - Ajouter une **anonymisation automatique** des champs sensibles (ex : adresses email, noms d'utilisateur, numéros de compte, etc.).
  - Vérifier que les logs ne transitent pas en clair et sont **chiffrés avant stockage**.

### 2.5. Absence de Mécanisme d’Alerte Automatique
- **Problème** : `SecuLogger` permet seulement d'écrire des logs, mais il ne **déclenche pas d'alertes** en cas d'événements critiques.
- **Action nécessaire** :
  - Ajouter une **intégration avec un système d’alerting** (ex : envoi d’un mail/slack en cas de `Fatal` ou `Error`).

### 2.6. Centralisation et Transmission des Logs
- **Problème** : Les logs sont actuellement stockés localement, ce qui rend difficile leur exploitation.
- **Action nécessaire** :
  - Ajouter une **capacité de transmission des logs** vers un serveur centralisé (ex: ELK, ELISA, ou une base SQL dédiée).
  - Permettre l’export des logs sous un format exploitable (`JSON`, `CSV`).

## 3. Modifications à Apporter dans `SecuLogger`
### 3.1. Nouvelle Structure des Logs
Chaque log devra inclure les champs suivants :
```json
{
  "timestamp": "2025-03-13T14:05:30Z",
  "level": "ERROR",
  "user_id": "M098391",
  "transaction_id": "7a82a0a6-ae18-49ce-b359-5c82a02f823b",
  "message": "Tentative de connexion échouée",
  "source": "AuthService",
  "stack_trace": "NullReferenceException at AuthService.Login()"
}

