# Action GitHub de Déploiement AKS

Ce workflow GitHub Action permet de déployer une application sur Azure Kubernetes Service (AKS).

## Prérequis

Avant de pouvoir utiliser cette action, assurez-vous de suivre les étapes suivantes :

![App registration](https://media.discordapp.net/attachments/1229408335204188190/1230495453292793866/image.png?ex=66338731&is=66211231&hm=39c5226419a41d73476650db979a843bd4492640d82faabc0c25d0da1141aaed&=&format=webp&quality=lossless)

1. Enregistrez votre application dans "App Registrations" sur Azure Active Directory.
2. Une fois l'enregistrement effectué, accédez à la section "Certifacts & secrets", puis à "Federal Credential".

!(https://media.discordapp.net/attachments/1229408335204188190/1230495519936086057/image.png?ex=66338741&is=66211241&hm=e537314deef51084a25a28d294fab467904c510fdcb244f7cce26ea3accbcba9&=&format=webp&quality=lossless&width=609&height=560)

3. Ajoutez votre dépôt GitHub comme dépôt autorisé à effectuer des actions dans "Federal Credential".
   - Organisation : Nom de votre organisation GitHub.
   - Repository : Nom de votre dépôt.
   - Entity type : "branch" et le nom de la branche qui déclenche l'action.

!(https://media.discordapp.net/attachments/1229408335204188190/1230496090529468416/Sans_titre_1.png?ex=663387c9&is=662112c9&hm=fd4877d132ea8cf0d3a2d9478488df9d5294e89a57dee6193f53b9101cf62582&=&format=webp&quality=lossless&width=1307&height=560)

!(https://media.discordapp.net/attachments/1229408335204188190/1230496273220636742/image.png?ex=663387f5&is=662112f5&hm=6de0829d184993767db1ed1d9ead98b8a224b8f1346cb0931af8837589a131d4&=&format=webp&quality=lossless&width=1307&height=560)

4. Récupérez le Client ID et le Tenant ID dans l'application registration sous l'onglet "Overview".

!(https://media.discordapp.net/attachments/1229408335204188190/1230495909712887910/Sans_titre.png?ex=6633879e&is=6621129e&hm=bed976a80efecd5e8f8a62f233ddf3de0718eaef99f21d16bb09a7be8f4e5850&=&format=webp&quality=lossless&width=1307&height=560)

5. Ajoutez ces informations dans les secrets de votre dépôt GitHub :
   - AZURE_CLIENT_ID : Client ID récupéré.
   - AZURE_TENANT_ID : Tenant ID récupéré.
   - AZURE_SUBSCRIPTION_ID : ID d'abonnement du service Kubernetes.

!(https://media.discordapp.net/attachments/1229408335204188190/1230496586833068052/Sans_titre_2.png?ex=6633883f&is=6621133f&hm=da01384a13367c682810914a52902398fba6aabb72383a090175a6ceebe7fc15&=&format=webp&quality=lossless&width=1264&height=560)

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

---

_Pour toute question ou assistance, veuillez contacter [votre_nom](lien_vers_votre_profil)._
