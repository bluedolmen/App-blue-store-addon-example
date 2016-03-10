# App-blue-store-addon-example

This repository contains code example to create your own addon for Blue AppStore so it can be easily install and share among the BlueDolmen &amp; Alfresco community

## Pre-requisities

In order to build and publish your addon to appstore.bluedolmen.com, you will need :
* An account on appstore.bluedolmen.com
* ant build tools
This repository provide a zip version of curl for windows.

With your bluedolmen account comes a specific user path you can use to publish your addons **org.bluedolmen.people.USERNAME.public** and **org.bluedolmen.people.USERNAME.private**
In this groupId there is two parts a *public* one and a *private*
For example, user1 can use **org.bluedolmen.people.user1.private** or **org.bluedolmen.people.USERNAME.public**
* private : only you can browse and install addons with this groupId
* public : everyone can browse and install the addon with this groupId

## How to create my own addon ?

In order to create your own addons you will need to :

* Clone this repository, for example in a Devel folder in your home directory (/home/ycoulon/Devel/App-blue-store-addon-example)
* Into the folder **src/addons** create the folder of your addons based on a the *groupId* and the *moduleId* you want to use, for example "org.bluedolmen.people.ycoulon.private.sample" become "org/bluedolmen/people/ycoulon/private/sample"
* Duplicate the META-INF folder located into *src/addons/org/bluedolmen/app/bluecourrier/custom/data* or *src/addons/org/bluedolmen/app/bluecourrier/custom/ui* into your addon folder.
* Edit the build.properties with your module information, for example 
```
addon.name=Sample
addon.groupId=org.bluedolmen.people.ycoulon.private
addon.moduleId=sample

addon.author=ycoulon
addon.email=ycoulon@bluedolmen.com
addon.category=/App/BlueDolmen/Sample

base=/home/ycoulon/Devel/App-blue-store-addon-example
```
* From now if you launch **ant package** a jar will be generated in the **dist** in your base folder (in this example /home/ycoulon/Devel/App-blue-store-addon-example)

## How to publish my addons ?

In order to publish your addon on **appstore.bluedolmen.com**, you will need to :
* Create a .build-bdas.properties file, this file will hold your appstore credentials. In this file you will put the following informations :
```
das.protocol=https
bdas.host=appstore.bluedolmen.com
bdas.user=<USERNAME>
bdas.passwd=<PASSWORD>
```
* From now you can publish to bluedolmen appstore running **publish** task.


## Issue

### **ant publish** fail with and 401 Unauthorized http code

This error seems to be linked with **curl** version. 
By default the build use the -u params to send credentials.
You update build-common.xml file to give credentials in URI instead of using -u params.
Comment line 123 and 131 of the build-common.xml file and uncomment line 124