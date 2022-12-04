CreateTopic
------------
docker exec -it kafka-1 kafka-topics --bootstrap-server localhost:9092       --replication-factor 1 --partitions 1 --create --topic topic01
docker exec -it kafka-1 kafka-topics --bootstrap-server kafka-1:9092         --replication-factor 1 --partitions 1 --create --topic topic02
docker exec -it kafka-1 kafka-topics --bootstrap-server kafka1.lan:9092      --replication-factor 1 --partitions 1 --create --topic topic03
docker exec -it kafka-1 kafka-topics --bootstrap-server 192.168.94.131:9092  --replication-factor 1 --partitions 1 --create --topic topic04
docker exec -it kafka-1 kafka-topics --bootstrap-server kafka3.lan:9092      --replication-factor 1 --partitions 1 --create --topic topic05

docker exec -it kafka-1 kafka-topics --bootstrap-server 192.168.94.131:9092,192.168.94.132:9092,192.168.94.133:9092      \
   --replication-factor 2 --partitions 5 --create --topic topic07

docker exec -it kafka-1 kafka-topics --bootstrap-server localhost:9092,broker1.lan:9092,broker2.lan:9092,broker3.lan:9092 \
   --replication-factor 3 --partitions 5 --create --topic topic08


Show Topic
-----------
docker exec -it kafka-1 kafka-topics --bootstrap-server 192.168.94.131:9092,192.168.94.132:9092,192.168.94.133:9092     --list
docker exec -it kafka-1 kafka-topics --bootstrap-server localhost:9092 --list


Delete Topic
-------------
docker exec -it kafka-1 kafka-topics --bootstrap-server localhost:9092 --delete --topic foo



Describe Topic
--------------
docker exec -it kafka-1 kafka-topics --bootstrap-server 192.168.94.131:9092,192.168.94.132:9092,192.168.94.133:9092     --describe


Create Producer
----------------
docker run -it --rm --network kafka_net confluentinc/cp-kafka /bin/kafka-console-producer --bootstrap-server kafka-1:9092 --topic topic02
docker exec -it kafka-3 kafka-console-producer --bootstrap-server localhost:9092 --topic topic02
docker exec -it kafka-2 kafka-console-producer --bootstrap-server kafka-1:9092   --topic topic02


Create Consumer
----------------
docker run -it --rm --network kafka_net confluentinc/cp-kafka /bin/kafka-console-consumer --bootstrap-server kafka-1:9092 --topic topic02 --from-beginning




List Metadata:
---------------
docker run -it --rm   --network host        edenhill/kcat:1.7.1                 -b   localhost:9092 -L
docker run -it --rm   --network kafka_net   edenhill/kcat:1.7.1                 -b  kafka1.lan:9092 -L
docker run -it --rm   --network kafka_net   confluentinc/cp-kafkacat   kafkacat -b  kafka1.lan:9092 -L



Producer:
docker run -it --rm \
  --network kafka_net \
  --name producer \
  edenhill/kcat:1.7.0 \
  -b kafka1.lan:9092 -P -t t1

docker run -it --rm \
  --network kafka_net \
  --name producer \
  confluentinc/cp-kafkacat \
  kafkacat \
  -b kafka1.lan:9092 -P -t t1

Consumer:
docker run -it --rm \
  --network kafka_net \
  --name consumer \
  edenhill/kcat:1.7.0 \
  -b kafka1.lan:9092 -C -t t1




https://github.com/confluentinc/schema-registry

docker exec  zookeeper-2 /bin/bash -c "echo "srvr" | nc localhost 2181  "
docker exec  zookeeper-1 /bin/bash -c "echo "srvr" | nc localhost 2181 | grep "Mode" "


echo "srvr" | nc localhost 2181
echo "mntr" | nc localhost 2181
echo "stat" | nc localhost 2181
echo "conf" | nc localhost 2181
echo "ruok" | nc localhost 2181
echo "isro" | nc localhost 2181

nc -zv localhost 2181


https://stackoverflow.com/questions/58563035/multiple-kafka-schema-registry-against-same-cluster

SCHEMA_REGISTRY_SCHEMA_REGISTRY_GROUP_ID 


docker-compose logs kafka-1 | grep -i started


# Client Connecting from the Same Docker Network
docker run -it --rm --network kafka_net confluentinc/cp-kafka /bin/kafka-console-producer --bootstrap-server kafka1.net:9092 --topic topic02
>hello
>world


# Client Connecting from the Same Host
kafka-console-producer --bootstrap-server localhost:9092 --topic topic02
>hi
>there


# Client Connecting from a Different Host
kafka-console-producer --bootstrap-server 192.168.94.131:9092 --topic topic02
>hello
>REMOTE SERVER




