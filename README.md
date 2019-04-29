# SmartStockExchange
This is an academic project focused on implementing online stock trading using blockchain technology.

## IMPLEMENTATION STEPS

### **Step 1:Installation step:-**

_1) Installing pre-requisites: -_

If you're running on Ubuntu, you can download the prerequisites using the following commands:
```bash
$ curl -O https://hyperledger.github.io/composer/v0.19/prereqs-ubuntu.sh
$ chmod u+x prereqs-ubuntu.sh
```
Next run the script - as this briefly uses sudo during its execution, you will be prompted for your password.
```bash
$ ./prereqs-ubuntu.sh
```
_2) Install the CLI tools_

There are a few useful CLI tools for Composer developers. The most important one is composer-cli, which contains all the essential operations, so we'll install that first. Next, we'll also pick up generator-Hyperledger-composer, composer-rest-server and Yeoman plus the generator-Hyperledger-composer. Those last 3 are not core parts of the development environment, but they'll be useful if you're following the tutorials or developing applications that interact with your Business Network, so we'll get them installed now.
Note that you should not use su or sudo for the following npm commands.
Essential CLI tools:
```sh
$ npm install -g composer-cli@0.19
```
Utility 	for running a REST Server on your machine to expose your business 	networks as RESTful APIs:
```
$ npm install -g composer-rest-server@0.19
```
Useful 	utility for generating application assets:
```
$ npm install -g generator-hyperledger-composer@0.19
```
Yeoman is a tool for generating applications, which utilises generator-Hyperledger-
composer:
```
$ npm install -g yo
```
_3) Install Hyperledger Fabric_

This step gives you a local Hyperledger Fabric runtime to deploy your business networks to.
In a directory of your choice (we will assume ~/fabric-dev-servers), 	get the .tar.gz file that contains the tools to install Hyperledger 	Fabric:
```
$ mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers
$ curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-
servers.tar.gztar -xvf fabric-dev-servers.tar.gz
```
A zip is also available if you prefer: just replace the .tar.gz file with fabric-dev-servers.zip and the tar -xvf command with a unzip command in the preceding snippet.
Use the scripts you just downloaded and extracted to download a local Hyperledger Fabric v1.1 runtime:
```
$ cd ~/fabric-dev-servers
$ export FABRIC_VERSION=hlfv11
$ ./downloadFabric.sh
```

### **Step 2:Controlling your dev environment:-**

Starting and stopping Hyperledger Fabric You control your runtime using a set of scripts which you'll find in ~/fabric-dev-servers if you followed the suggested defaults.
The first time you start up a new runtime, you'll need to run the start script, then generate a Peer Adm card:
```
$ cd ~/fabric-dev-servers
$ export FABRIC_VERSION=hlfv11
```
```
$ ./startFabric.sh
$ ./createPeerAdminCard.sh
```

### **Step 3:Download Source code:-**

```
$ git clone https://github.com/pasadyash/SmartStockExchange.git
```

### **Step 4:Deploying the business network**

In new terminal run below commands 
Navigate in the SmartStockExchange/stbc-network folder

_1) Setting up admin REST server_

```
$ npm install 
$ composer network install --card PeerAdmin@hlfv1 --archiveFile stbc- network@0.0.1.bna
```
The composer network install command requires a PeerAdmin business network card (in this case one has been created and imported in advance), and the the file path of the .bna which defines the business network.
To start the business network, run the following command:
```
$ composer network start --networkName stbc-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card
```
The composer network start command requires a business network card, as well as the name of the admin identity for the business network, the name and version of the business network and the name of the file to be created ready to import as a business network card.
To import the network administrator identity as a usable business network card, run the following command:
```
$ composer card import --file networkadmin.card
```
The composer card import command requires the filename specified in composer network start to create a card.
To check that the business network has been deployed successfully, run the following command to ping the network:
```
$ composer network ping --card admin@stbc-network
```

Or
Simply run shell script command 
```
$ ./networkStart.sh stbc-network amin 0.0.4
```

_2) Generating a multi-user REST server:_

In new terminal run below commands 
Navigate in the SmartStockExchange/stbc-network folder

```
$ ./rsmulti.sh  -d local -a google
```

_3) Run client application:_

In new terminal run below commands 
Navigate in the SmartStockExchange/stbc-app/server folder

```
$ npm install 
$ node app.js
```
