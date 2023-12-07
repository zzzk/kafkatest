# k a f k a t e s t 

## setup operator

```
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka
```

## setup cluster

kubectl apply -f https://raw.githubusercontent.com/zzzk/kafkatest/main/strimzi.yaml -n kafka 

## write to topic

kubectl -n kafka run kafka-producer -ti --image=quay.io/strimzi/kafka:0.38.0-kafka-3.6.0 --rm=true --restart=Never -- bin/kafka-console-producer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic

## read from topic

kubectl -n kafka run kafka-consumer -ti --image=quay.io/strimzi/kafka:0.38.0-kafka-3.6.0 --rm=true --restart=Never -- bin/kafka-console-consumer.sh --bootstrap-server my-cluster-kafka-bootstrap:9092 --topic my-topic --from-beginning

## delete the cluster

kubectl -n kafka delete $(kubectl get strimzi -o name -n kafka)

