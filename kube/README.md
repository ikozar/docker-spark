## setup
install k8s-spark-cluster-ds.yaml
install spark-ingress.yaml
spark-nodeport.yaml if you want to run spark-submit from local host (or add master endpoint to ingress)
check http://spark-kubernetes/

## submit from master pod

export SPARK_HOME=/spark
export SPARK_DIST_CLASSPATH="$SPARK_HOME/jars/*"

./bin/spark-submit \
  --class org.apache.spark.examples.SparkPi \
  --master spark://spark-master-f97654757-226qt:7077 \
  local:///spark/examples/jars/spark-examples_2.11-2.4.5.jar \
  1000
  
## submit from host PC
1. from linux
    download https://archive.apache.org/dist/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz and unpack tp /spark
    submit as from master pod
2. from WIN10
    - set env SPARK_USER=ikozar
    - add -Duser.name=ikozar
    java -Xmx1g -cp "d:/spark-2.4.5-bin-hadoop2.7/conf/;d:/spark-2.4.5-bin-hadoop2.7/jars/*"
         org.apache.spark.deploy.SparkSubmit
         --master spark://<k8s ip>:30077 <port from nedeport svc>
         --class org.apache.spark.examples.SparkPi
         local:///d:/spark-2.4.5-bin-hadoop2.7/examples/jars/spark-examples_2.11-2.4.5.jar 1000
    try to find http point to download examples and replace resource with http:
