schema-registry
===============
Schema registry for Kafka

Quickstart
----------

1. Start ZooKeeper from the standard Kafka install
./bin/zookeeper-server-start.sh config/zookeeper.properties

2. Start Kafka from the standard Kafka install
./bin/kafka-server-start.sh config/server.properties

3. Start the REST server by running io.confluent.kafka.schemaregistry.rest.Main
mvn exec:java -Dexec.mainClass="io.confluent.kafka.schemaregistry.rest.Main" -Dexec.args="config/schema-registry.properties"

4. Register a schema
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X POST -i http://localhost:8080/subjects/Kafka/versions -d '{"schema": "{\"type\": \"string\"}"}'

curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X POST -i http://localhost:8080/subjects/Kafka,key/versions -d '{"schema": "{\"type\": \"string\"}"}'

5. List all subjects 
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X GET http://localhost:8080/subjects

6. List all versions of a subject's schema
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X GET http://localhost:8080/subjects/Kafka/versions

7. Get a particular version of a subject's schema
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X GET http://localhost:8080/subjects/Kafka/versions/1

8. Get top level config
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X GET http://localhost:8080/config

9. Update compatibility level globally
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X PUT -i http://localhost:8080/config -d '{"compatibility":"NONE"}'

10. Deprecate a particular version of a subject's schema
curl -v -H "Content-Type: application/vnd.schemaregistry.v1+json" -X DELETE http://localhost:8080/subjects/Kafka/versions/1
