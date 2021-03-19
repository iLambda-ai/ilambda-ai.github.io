-------------------------------------------------------
# INSTRUCTIONS
-------------------------------------------------------
0. source:
https://github.com/iLambda-ai/EDA3/blob/k8s_eda3/management/k8s/ilambda_images/config/ilambda.properties
https://github.com/iLambda-ai/EDA3/blob/k8s_eda3/management/k8s/ilambda/eda_deployment.yaml
https://ilambda.atlassian.net/wiki/spaces/MAN/pages/833323092/SCU+and+CCU+Configurations

**Pre-requisites**

1. Create a config map with information on hosts to ip address mapping to be copied to /etc/hosts inside the pods
  - Create a file with hosts to ip mapping (e.g. hosts.cluster)
  - Create a config map by using the following command in the same namespace where eda-cloud setup is to be done.
  kube create configmap host-file-config-map --from-file hosts.cluster
2. Update the values.yaml file with cluster specific information (e.g. in case of installation in fra cluster )
  - global.hostFileConfigMap: host-file-config-map (The name of the config map created in step 1)
  - zk.host : fra-b-bi-sp01:2181
  - global.imageRepo: Can be either of the values mentioned below
    - artifactory.ilambda.com/docker-dev (from jfrog artifactory)
    - fra-b-bi-sp08:5000 (local registry)
  - global.imagePullSecrets: jfrog-docker-secret (Required if the imageRepo above points to artifactory)
  - global.dockerSecret: Use the script scripts/generate_docker_secrets.sh to generate a hash of the docker authentication
    and attach the hash to this variable. (Required if the imageRepo above points to artifactory)
    e.g. bash scripts/generate_docker_secrets.sh admin admin
  - pushgatewayUrl: The url of the pushgateway server of the prometheus

  Note: All these parameters above can also be set during helm install command by using the --set argument
    e.g. helm install --name=ccu-test local/eda-cloud --set zk.host=fra-b-bi-sp01:2181,global.imageRepo=fra-b-bi-sp08:5000

**tutorial**
0. how to start from local repo
helm install local/eda-cloud --version 1.0.0 --name eda-office-test
helm install local/eda-cloud --version 1.0.0 --name eda-office-test --set userId=${CUSTOMER_ID}
helm install local/eda-cloud --version 1.1.0 --name eda-office-test --set userId=eric_chu
helm install local/eda-cloud --name ccu-testuser2 --set userId=ccu-testuser2

helm install local/eda-cloud --name ccu-testuser2 --set userId=ccu-testuser2,zk.host=10.106.192.112:2181,edakafka.imageRepo=ilambda1:5000,mongo.imageRepo=ilambda1:5000,postgres.imageRepo=ilambda1:5000,imageRepo=ilambda1:5000
helm install local/eda-cloud --name ccu-testuser2 --set userId=ccu-testuser2,zk.host=192.168.1.16:2181,edakafka.imageRepo=ilambda1:5000,mongo.imageRepo=ilambda1:5000,postgres.imageRepo=ilambda1:5000,imageRepo=ilambda1:5000
bash delete_project_pv.sh ccu-testuser2; bash delete_available_pvs.sh; bash generate_pv_new.sh eda-eric-test 10

1. how to upgrade exist deployment
helm upgrade ccu-testuser2 local/eda-cloud
helm package .
helm dependency update
helm delete --purge $p

how to update helm local repo
rm -rf ~/.helm/cache/archive/*
rm -rf ~/.helm/repository/cache/*

how to delete current project pvc/pv
p=eda-eric-test
kube get pvc | awk -v p=$p '{if ($1~p) print $1}' | xargs -I{} kubectl delete pvc {}
kube get pv | awk -v p=$p '{if ($6~p && $5="Released") print $1}' | xargs -I{} bash delete_one_pv.sh {}

-------------------------------------------------------
# TODO:
-------------------------------------------------------
0. stress testing with JMeter
0. create global scrip configmap for script lib

6. make personal ci/cd into helm

- - - - - - - - - - - - - - - - - - - - - - -
# Helm Install
- - - - - - - - - - - - - - - - - - - - - - -
1. How to install helm
   a. curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
   b. bash get_helm.sh
   c. kubectl -n kube-system create sa tiller
   d. kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
   e. helm init --service-account tiller

2. helm pakcage
3. use subchart
   helm dep update ./chart

4. uninstall
   helm reset

- - - - - - - - - - - - - - - - - - - - - - -
# EDA Cloud Install
- - - - - - - - - - - - - - - - - - - - - - -
How to install at a new environment
0. enable local storage - one time:
   kube create -f local-storage-class.yml
1. create local storage
2. enable helm server
   helm serve
3. prepare module helm installer
   helm package .
4. install a individual zookeeper as SCU
   helm install local/zk-cluster --name eda-scu-zk
5. install a individual postgres
   helm install local/postgre-sql-cluster --name eda-share-postgres
6. configure SCU
   use docker image to use the zkCli.sh
   create /ilambda/cloud/default/CCU
   bash create_zk_node.sh $ZK_HOST /ilambda/cloud/default/SCU $CONFIG_FILE

7. build all images
   a. build eda_image
   b. build mongs_image
8. prepare mongs helm installer
9. update all repo info
    - data_load/eda-cloud/values.yaml:65:  repository: ilambda1:5000/eda-zk-init
    - data_load/eda-cloud/values.yaml:70:  container: ilambda1:5000/eda
    - data_load/eda-cloud/values.yaml:75:  container: ilambda1:5000/eda-core-table-data-loader
    - data_load/eda-cloud/values.yaml:80:  container: ilambda1:5000/eda-event-log-data-loader
    - data_load/eda-cloud/values.yaml:84:  container: ilambda1:5000/eda-data-collector
    - data_load/eda-cloud/values.yaml:89:  container: ilambda1:5000/eda-web-portal
    - data_load/kafka-cluster/values.yaml:40:  repository: ilambda1:5000/kafka-2-12-ubuntu
    - mongo_cluster/mongs-server-mongo-db-deployment/mongs-deployment/values.yaml:39:  repository: ilambda1:5000/ilambda-mongos-service
10. launch system
   helm install local/eda-cloud --name ccu-testuser2 --set userId=ccu-testuser2,zk.host=10.106.192.112:2181
   - 10.106.192.112 is the SCU ZK address



-------------------------------------------------------
# DEBUG:
-------------------------------------------------------
kafka_broker_ip=localhost
/opt/kafka/bin//kafka-consumer-groups.sh --describe --group eda_event_log_loader-event_log --bootstrap-server $kafka_broker_ip:6667
/opt/kafka/bin//kafka-consumer-groups.sh --describe --group eda_core_table_data_loader-original_item --bootstrap-server $kafka_broker_ip:6667
/opt/kafka/bin//kafka-consumer-groups.sh --describe --group eda_core_table_data_loader-item_stats --bootstrap-server $kafka_broker_ip:6667

-------------------------------------------------------
# UPGRADE:
-------------------------------------------------------
----- for SCU -----
p=scu-ilambda1
c="local/system-service"
helm upgrade $p $c --set edakafka.extraVars[0].name=KAFKA_HEAP_OPTS,edakafka.extraVars[0].value="-Xmx256M -Xms128M",edakafka.extraVars[1].name=KAFKA_OPTS,edakafka.extraVars[1].value="-Dlogging.level=WARN" --reuse-values

----- for CCU -----
p=ccu-banggood
c="local/eda-cloud"
v="1.3.0"

helm upgrade $p $c --version=$v --set edakafka.extraVars[0].name=KAFKA_HEAP_OPTS,edakafka.extraVars[0].value="-Xmx256M -Xms128M",edakafka.extraVars[1].name=KAFKA_OPTS,edakafka.extraVars[1].value="-Dlogging.level=WARN" --reuse-values
