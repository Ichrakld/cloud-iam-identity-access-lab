# Catalogue des preuves — identité IAM

Les captures sont reproduites depuis les preuves communiquées, renommées descriptivement. Les codes TOTP de la capture 25 ont été masqués ; le secret MFA et les clés privées ne sont pas inclus.

### 01-localstack-demarrage-docker

**Original :** `Screenshot 2026-10-19 115625.png`  
**Preuve :** [Démarrage de LocalStack avec ENFORCE_IAM=1](../evidence/01-environnement/01-localstack-demarrage-docker.png)

Le conteneur est lancé avec l’application des permissions IAM demandée par le laboratoire. L’option doit être vérifiée par un test de refus réel.

![Démarrage de LocalStack avec ENFORCE_IAM=1](../evidence/01-environnement/01-localstack-demarrage-docker.png)

### 02-docker-conteneur-localstack

**Original :** `Screenshot 2026-10-19 115648.png`  
**Preuve :** [État du conteneur Docker](../evidence/01-environnement/02-docker-conteneur-localstack.png)

Le conteneur LocalStack apparaît actif et expose le port 4566 sur l’interface locale.

![État du conteneur Docker](../evidence/01-environnement/02-docker-conteneur-localstack.png)

### 03-localstack-verification-health

**Original :** `Screenshot 2026-10-19 115717.png`  
**Preuve :** [État de santé des services](../evidence/01-environnement/03-localstack-verification-health.png)

L’API /_localstack/health répond ; la disponibilité des services ne démontre pas à elle seule l’application des politiques IAM.

![État de santé des services](../evidence/01-environnement/03-localstack-verification-health.png)

### 04-configuration-aws-cli-localstack

**Original :** `Screenshot 2026-10-19 115956.png`  
**Preuve :** [Configuration AWS CLI](../evidence/01-environnement/04-configuration-aws-cli-localstack.png)

Identifiants de test et endpoint local 127.0.0.1:4566 : les opérations ciblent l’émulateur, pas AWS en production.

![Configuration AWS CLI](../evidence/01-environnement/04-configuration-aws-cli-localstack.png)

### 05-sts-identite-administrateur

**Original :** `Screenshot 2026-10-19 120037.png`  
**Preuve :** [Identité STS de l’administrateur](../evidence/01-environnement/05-sts-identite-administrateur.png)

STS renvoie l’ARN root du compte simulé 000000000000.

![Identité STS de l’administrateur](../evidence/01-environnement/05-sts-identite-administrateur.png)

### 06-identifiant-compte-simule

**Original :** `Screenshot 2026-10-19 120046.png`  
**Preuve :** [Identifiant du compte](../evidence/01-environnement/06-identifiant-compte-simule.png)

Le numéro de compte local 000000000000 est stocké dans ACC pour construire les ARN IAM.

![Identifiant du compte](../evidence/01-environnement/06-identifiant-compte-simule.png)

### 07-creation-utilisateur-controle

**Original :** `Screenshot 2026-10-19 120117.png`  
**Preuve :** [Création de controle](../evidence/02-identites-et-profils/07-creation-utilisateur-controle.png)

Un utilisateur sans politique IAM est créé pour tester le refus par défaut.

![Création de controle](../evidence/02-identites-et-profils/07-creation-utilisateur-controle.png)

### 08-creation-cle-controle

**Original :** `Screenshot 2026-10-19 120203.png`  
**Preuve :** [Clé d’accès de controle](../evidence/02-identites-et-profils/08-creation-cle-controle.png)

Une clé d’accès est créée ; les valeurs sont capturées dans des variables sans afficher la clé secrète.

![Clé d’accès de controle](../evidence/02-identites-et-profils/08-creation-cle-controle.png)

### 09-profil-aws-controle

**Original :** `Screenshot 2026-10-19 120210.png`  
**Preuve :** [Profil CLI de controle](../evidence/02-identites-et-profils/09-profil-aws-controle.png)

Le profil AWS CLI utilise les identifiants propres à controle pour séparer l’authentification administrateur et utilisateur.

![Profil CLI de controle](../evidence/02-identites-et-profils/09-profil-aws-controle.png)

### 10-controle-s3-refus-acces

**Original :** `Screenshot 2026-10-19 120257.png`  
**Preuve :** [Refus S3 pour controle](../evidence/03-autorisations/10-controle-s3-refus-acces.png)

La requête s3:ListAllMyBuckets échoue avec AccessDenied : preuve de l’implicit deny.

![Refus S3 pour controle](../evidence/03-autorisations/10-controle-s3-refus-acces.png)

### 11-sts-identite-controle

**Original :** `Screenshot 2026-10-19 120440.png`  
**Preuve :** [STS de controle](../evidence/02-identites-et-profils/11-sts-identite-controle.png)

STS confirme l’ARN user/controle : authentification réussie, sans autorisation S3.

![STS de controle](../evidence/02-identites-et-profils/11-sts-identite-controle.png)

### 12-nettoyage-controle

**Original :** `Screenshot 2026-10-19 120606.png`  
**Preuve :** [Suppression du compte de contrôle](../evidence/02-identites-et-profils/12-nettoyage-controle.png)

La clé d’accès de controle et l’utilisateur de test sont supprimés.

![Suppression du compte de contrôle](../evidence/02-identites-et-profils/12-nettoyage-controle.png)

### 13-creation-alice-bob-claire

**Original :** `Screenshot 2026-10-19 120633.png`  
**Preuve :** [Création des utilisateurs IAM](../evidence/02-identites-et-profils/13-creation-alice-bob-claire.png)

Alice (data), Bob (audit) et Claire (reseau) sont créés avec leurs tags team.

![Création des utilisateurs IAM](../evidence/02-identites-et-profils/13-creation-alice-bob-claire.png)

### 14-inventaire-utilisateurs

**Original :** `Screenshot 2026-10-19 120700.png`  
**Preuve :** [Liste des utilisateurs](../evidence/02-identites-et-profils/14-inventaire-utilisateurs.png)

La commande list-users confirme l’existence des trois identités IAM.

![Liste des utilisateurs](../evidence/02-identites-et-profils/14-inventaire-utilisateurs.png)

### 15-sts-alice-authentification

**Original :** `Screenshot 2026-10-19 120815.png`  
**Preuve :** [Authentification d’Alice](../evidence/02-identites-et-profils/15-sts-alice-authentification.png)

Le profil Alice est reconnu par STS ; cette identité n’a pas encore de droit S3.

![Authentification d’Alice](../evidence/02-identites-et-profils/15-sts-alice-authentification.png)

### 16-creation-groupes-iam

**Original :** `Screenshot 2026-10-19 120854.png`  
**Preuve :** [Création des groupes](../evidence/03-autorisations/16-creation-groupes-iam.png)

Les groupes developpeurs, auditeurs et admins-reseau sont créés.

![Création des groupes](../evidence/03-autorisations/16-creation-groupes-iam.png)

### 17-affectation-groupes-iam

**Original :** `Screenshot 2026-10-19 120929.png`  
**Preuve :** [Affectation des utilisateurs](../evidence/03-autorisations/17-affectation-groupes-iam.png)

Alice appartient à developpeurs, Bob à auditeurs et Claire à admins-reseau.

![Affectation des utilisateurs](../evidence/03-autorisations/17-affectation-groupes-iam.png)

### 18-s3-alice-refus-par-defaut

**Original :** `Screenshot 2026-10-19 121012.png`  
**Preuve :** [Bucket et refus d’Alice](../evidence/03-autorisations/18-s3-alice-refus-par-defaut.png)

Le bucket tp-iam-ichrak est créé par l’administrateur ; Alice obtient AccessDenied sur le listing.

![Bucket et refus d’Alice](../evidence/03-autorisations/18-s3-alice-refus-par-defaut.png)

### 19-politique-s3-lecture-seule-auditeurs

**Original :** `Screenshot 2026-10-19 121048.png`  
**Preuve :** [Politique de lecture seule](../evidence/03-autorisations/19-politique-s3-lecture-seule-auditeurs.png)

AmazonS3ReadOnlyAccess est attachée au groupe auditeurs, dont Bob est membre.

![Politique de lecture seule](../evidence/03-autorisations/19-politique-s3-lecture-seule-auditeurs.png)

### 20-tests-s3-bob-alice

**Original :** `Screenshot 2026-10-19 121255.png`  
**Preuve :** [Comparaison des droits](../evidence/03-autorisations/20-tests-s3-bob-alice.png)

Bob peut lister les buckets mais sa tentative de création échoue ; Alice reste refusée.

![Comparaison des droits](../evidence/03-autorisations/20-tests-s3-bob-alice.png)

### 21-application-politique-mots-de-passe

**Original :** `Screenshot 2026-10-19 121320.png`  
**Preuve :** [Définition de la politique](../evidence/04-mots-de-passe/21-application-politique-mots-de-passe.png)

Configuration demandant au moins 14 caractères, un historique de 5 mots de passe et aucune expiration forcée.

![Définition de la politique](../evidence/04-mots-de-passe/21-application-politique-mots-de-passe.png)

### 22-verification-politique-mots-de-passe

**Original :** `Screenshot 2026-10-19 121338.png`  
**Preuve :** [Vérification de la politique](../evidence/04-mots-de-passe/22-verification-politique-mots-de-passe.png)

La réponse IAM confirme MinimumPasswordLength=14, PasswordReusePrevention=5 et ExpirePasswords=false.

![Vérification de la politique](../evidence/04-mots-de-passe/22-verification-politique-mots-de-passe.png)

### 23-installation-oathtool

**Original :** `Screenshot 2026-10-19 122234.png`  
**Preuve :** [Installation oathtool](../evidence/05-mfa/23-installation-oathtool.png)

Installation de l’outil permettant de calculer des codes TOTP dans le laboratoire.

![Installation oathtool](../evidence/05-mfa/23-installation-oathtool.png)

### 24-creation-appareil-mfa-virtuel

**Original :** `Screenshot 2026-10-19 122310.png`  
**Preuve :** [Création du MFA virtuel](../evidence/05-mfa/24-creation-appareil-mfa-virtuel.png)

L’appareil alice-mfa est créé et son ARN apparaît ; le secret Base32 reste privé.

![Création du MFA virtuel](../evidence/05-mfa/24-creation-appareil-mfa-virtuel.png)

### 25-activation-mfa-codes-expurges

**Original :** `Screenshot 2026-10-19 122859.png`  
**Preuve :** [Activation MFA (codes masqués)](../evidence/05-mfa/25-activation-mfa-codes-expurges.png)

Commande d’activation du MFA pour Alice. Les deux codes TOTP présents dans l’original ont été intégralement masqués.

![Activation MFA (codes masqués)](../evidence/05-mfa/25-activation-mfa-codes-expurges.png)

### 26-verification-mfa-alice

**Original :** `Screenshot 2026-10-19 122931.png`  
**Preuve :** [Vérification du MFA](../evidence/05-mfa/26-verification-mfa-alice.png)

list-mfa-devices atteste l’enrôlement du dispositif alice-mfa pour Alice.

![Vérification du MFA](../evidence/05-mfa/26-verification-mfa-alice.png)

### 27-rapport-identites-iam

**Original :** `Screenshot 2026-10-19 123021.png`  
**Preuve :** [Rapport des identifiants](../evidence/06-inventaire/27-rapport-identites-iam.png)

Le credential report liste les champs user, mfa_active et access_key_1_active.

![Rapport des identifiants](../evidence/06-inventaire/27-rapport-identites-iam.png)

### 28-confirmation-rapport-identites

**Original :** `Screenshot 2026-10-19 123139.png`  
**Preuve :** [Confirmation de l’inventaire](../evidence/06-inventaire/28-confirmation-rapport-identites.png)

L’inventaire confirme Alice MFA=true, Bob/Claire MFA=false, et des clés d’accès actives pour les trois comptes.

![Confirmation de l’inventaire](../evidence/06-inventaire/28-confirmation-rapport-identites.png)

