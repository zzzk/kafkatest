# Kafkatest

## create the namespace
```
kubectl create namespace kafka
```

## setup operator
```
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka
```

## setup cluster
```
kubectl apply -f https://raw.githubusercontent.com/zzzk/kafkatest/main/strimzi.yaml -n kafka 
```

## write to topic
```
kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.45.0-kafka-3.9.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic
``` 

## read from topic
```
kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.45.0-kafka-3.9.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning
```

## delete the cluster
```
kubectl -n kafka delete $(kubectl get strimzi -o name -n kafka)
```

## delete the pcvs
```
kubectl delete pvc -l strimzi.io/name=my-cluster-kafka -n kafka
```

## delete the operator
```
kubectl -n kafka delete -f 'https://strimzi.io/install/latest?namespace=kafka'
```

## delete the namespace
```
kubectl delete namespace kafka
```