# Action GitHub de Déploiement AKS

Ce workflow GitHub Action permet de déployer une application sur Azure Kubernetes Service (AKS).

## Prérequis

Avant de pouvoir utiliser cette action, assurez-vous de suivre les étapes suivantes :

1. Enregistrez votre application dans "App Registrations" sur Azure Active Directory.
2. Une fois l'enregistrement effectué, accédez à la section "Certifacts & secrets", puis à "Federal Credential".
3. Ajoutez votre dépôt GitHub comme dépôt autorisé à effectuer des actions dans "Federal Credential".
   - Organisation : Nom de votre organisation GitHub.
   - Repository : Nom de votre dépôt.
   - Entity type : "branch" et le nom de la branche qui déclenche l'action.
4. Récupérez le Client ID et le Tenant ID dans l'application registration sous l'onglet "Overview".
5. Ajoutez ces informations dans les secrets de votre dépôt GitHub :
   - AZURE_CLIENT_ID : Client ID récupéré.
   - AZURE_TENANT_ID : Tenant ID récupéré.
   - AZURE_SUBSCRIPTION_ID : ID d'abonnement du service Kubernetes.

## Utilisation

Ce workflow s'exécute automatiquement sur les événements de push ou de pull request sur la branche principale (main).

### Permissions

- id-token : write
- contents : read

### Jobs

#### build-and-deploy

Ce job s'exécute sur une machine virtuelle Ubuntu.

1. **Set NameSpace** : Définit l'espace de noms en fonction de l'utilisateur GitHub.
2. **Set Trigram** : Définit le trigramme en fonction de l'utilisateur GitHub.
3. **Az CLI login** : Connexion à Azure CLI en utilisant les identifiants récupérés dans les secrets.
4. **Run checkout** : Récupère le code du dépôt.
5. **Set up Azure CLI** : Configure l'interface de ligne de commande Azure.
6. **Build and push Docker image** : Construit et pousse l'image Docker sur Azure Container Registry.
7. **Deploy to AKS** : Déploie l'application sur AKS.

