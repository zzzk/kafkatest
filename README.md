��#   k a f k a t e s t 

#setup operator
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka


#setup cluster
kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka 

#write to topic

#read from topic


#delete
kubectl -n kafka delete $(kubectl get strimzi -o name -n kafka)

