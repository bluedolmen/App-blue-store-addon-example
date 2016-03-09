# Offre

BlueDolmen met à votre disposition son appstore Alfresco pour enrichir votre installation en ajoutant en quelques instants des modules de gestion, de statistiques...

2 souscriptions sont disponibles :
* gratuites, pour une utilisation publique. Tout ce que vous publiez est disponible pour la communauté BlueDolmen (= globalement la communauté Alfresco Communautaire + Enterprise)
* payantes, pour une utilisation privée. Ce que vous publiez est privé et reste confidentiel.

Dans les 2 cas, le mécanisme de développement est le même.

Cf bluedolmen/webinaire/appstore-gettingstarted

# Installation et configuration

Cette installation doit vous permettre de construire des modules fonctionnels pour Alfresco que vous pourrez facilement gérer (éditer, versionner...), tester, déployer et partager.

Par module fonctionnel, on signifie des modules de haut niveau qui peuvent être configurés dynamiquement par simple dépôt de fichiers dans le repository. Ce peut être des contenus, des webscripts, des fichiers de configuration Alfresco (modèles, formulaires, processus, plans de classement), BlueDolmen (mise à jour automaique, mapping, règles de gestion) ou toute autre fonction que vous aurez développé capable de prendre des fichiers de configuration dans le repository.

Insert get-started

## Architecture

L'objectif est de pouvoir travailler avec un source géré par un éditeur spécialisé autre qu'Alfresco. En effet, il est difficile de faire du multifenêtrage, mutlti-onglets et de bénéficier également de fonctions de gestion de versions, de colorations syntaxique... S'il existe des éditeurs en mode cloud, notamment c9, elles sont payantes et ne sont pas encore entrées dans les moeurs.

Plusieurs éléments sont présents dans ce schéma :
* Les sources de votre module. Ces sources seront déployés in fine dans le repository Alfresco. Ils peuvent pour les tests être parfois déployés dans le système de fichiers de votre Alfresco, par exemple sous tomcat/webapps/alfresco/WEB-INF/classes/alfresco/webscripts/extension... 
* Le système Alfresco de test. Il est généralement installé sur votre machine. Vous pouvez faire cette installation sur une VM (Vagrant, docker ou autre...). Ce peut être un Alfresco Community ou Enterprise.
* L'appstore bluedolmen
* Les systèmes Alfresco de pré-prod et de prod

Le cycle de vie d'un module réalisé avec BlueDolmen est le suivant :

Insert images/bluedolmen-dev-steps.png

1 - Edition, versionning (svn, git...) puis copie des sources sur Alfresco dans le système de fichiers afin de pouvoir tester votre module. Les fichiers js copiés par exemple dans tomcat/webapps/alfresco/WEB-INF/classes/alfresco/webscripts/extension peuvent être importés immédiatement sans redémarrer quoique ce soit. Selon votre cas d'utilisation, il est parfois nécessaire de recharger les webservices afin qu'Alfresco identifie qu'un nouveau service est disponible
2 - Une fois satisfait(e) de votre développement, vous le packagez avec BlueDolmen SDK. Cela consiste à lancer un script Ant qui va construire un package .jar avec toutes les ressources définissant votre module, ainsi que quelques informations permettant son classement dans BlueDolmen Appstore
3 - Publication sur l'appstore. Le module est maintenant disponible pour les différents utilisateurs.
4 - Après avoir supprimé tous les éléments que aviez copiés dans Alfresco, vous déploiyez en quelques secondes votre module afin de pouvoir le tester sur votre serveur Alfresco de développement.
5 - Vous déployez le module sur le serveur de pré-production afin de pouvoir effectuer votre recette 
6 - Vous déployez le module sur le serveur de production afin qu'il soit utilisé par tous vos utilisateurs 

A partir de la version X.Y de BlueDolmen Appstore, il est possible de travailler avec votre appstore privé, vous permettant de déployer des contenus confidentiels, l'appstore public proposant les contenus à tous les utilisateurs. L'appstore permet de mutualiser et partager les efforts et investissements de chacun. Il est parfois nécessaire de garder des informations et/ou du code privés pour des raisons de confidentialité (organigramme avec n° tél), sécurité (documents de référence), juridique (liste de mail).

## Installation

Installer curl.exe dans ${base}/local/bin/curl.exe
Création d'un fichier .build-bdas.properties permettant de stocker les informations nécessaires à la connexion.

    base=/opt/local/git-workspaces/bluedolmen-appstore-addons
    bdas.user=admin
    bdas.passwd=XXXX

## Configuration

Le fichier build-synchro.xml

# Créer un nouveau module

* Copiez/Collez un projet existant
* Stockez ce nouveau projet dans l'arborescence adéquate (conventions java)
* Modifiez le fichier META-INF/build.properties pour indiquer son nom et les informations de classement
* Modifiez le fichier META-INF/module.yml.tpl qui permettra de générer le fichier module.yml : attention à ne jamais modifier directement le fichier META-INF/module.yml car il est regénéré à chaque fois !
* Modifiez le contenu du module
* Modifiez le fichier META-INF/file-mapping.properties pour refléter les répertoires où vous voulez stocker les répertoires et documents.

# Packaging

Positionnez-vous sur META-INF/build.xml
Lancez la target Package and publish

# Débogage

## Mise à jour de modèles de données

En mode développement, le plus simple est de supprimer tous les documents, et les supprimer de la corbeille également.
En mode production, il peut être nécessaire de faire la mise à jour manuelle des modèles de données. Eventuellement, 

## Mise à jour des formulaires

Mettre à jour les modules via la marketplace.
Aller sur le formulaire. S'il ne s'affiche pas correctement, notamment sans aucun formattage, affichez-le une nouvelle fois. Il devrait être correct. Si les labels des messages ne sont pas corrects, la clé apparaissant à la place du message lui-même, 

## Débogage des scripts js

Mise à jour de log4j.properties (Script = debug)
 