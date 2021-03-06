StormCharmConnector
===================

The storm charm connector is a library used by the StormDeployer subordinate Juju charm that provides a Storm bolt, spout, etc. with the host, port, user, password, etc. for the services that are related to the subordinate charm.

StormDeployer
=============

The storm deployer is a tool to deploy topologies to a Storm cluster that was deployed via Juju.
Deployment is possible via source code or via jar. A .storm yaml file is needed with deploy configurations. An example can be seen [here](https://github.com/xannz/WordCountExample).

Deploying with source code requires a .stom with the format:
```
topology:
    - name: name of the topology
      jar: jar of the topology
      topologyclass: full domain and class of the topology
      packaging: mvn package 
      repository: the git url where the topology can be found
      scriptbeforepackaging: optional script to run before packaging
      scriptbeforedeploying: optional script to run before deployment
      datasources:
      - parameters:
        - {name: name1, value: value1}
        - {name: name2, value: value2}
        type: type, can my mysql/mongo/postgres/redis/kafka/etc.
        script: script to execute
    - name: another topology
```

Deploying with jar requires a .storm with the format:
```
topology:
    - name: WordCountTopology
      jar: WordCountExample-1.0-SNAPSHOT.jar
      topologyclass: com.sborny.wordcountexample.WordCountTopology
      packaging: jar
      repository: https://github.com/xannz/WordCountExample.git
      release: https://github.com/xannz/WordCountExample/releases/download/1.0/WordCountExample-1.0-SNAPSHOT.jar
```

Deploying from a private repository requires username and password wich can be entered as credentials in the config:
```
juju set stormdeployer "credentials=username:password"
juju set stormdeployer "deploy=[url to .storm file on github]"
juju set stormdeployer "undeploy=TopologyName"
```
