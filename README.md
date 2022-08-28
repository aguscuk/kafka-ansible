# Kafka-Cluter Deployment

## Pre-requisite
cd kafka-cluter/
```sh
  sudo apt-get install python3-pip
  sudo pip3 install virtualenv
  virtualenv .venv
  source .venv/bin/activate
  pip3 install -r requirements.txt
```

## Quickstart
### Re-check config files
- ip addresses in inventory/development/hosts, check in [clusterNodes]
- ip addresses in inventory/development/group_vars/all.yml [kafkaZookeeperAddressString]


### Checking hosts
```sh
cd kafka/
  ansible -i inventory/development/ -m ping all
```
```sh
cd zookeeper/
  ansible -i inventory/development/ -m ping all
```

# Zookeeper deployment
* dry-run test
```sh
  ansible-playbook -i inventory/development/ clusterSetup.yml -C -v
```

* Run deployment
```sh
  ansible-playbook -i inventory/development/ clusterSetup.yml -v
```

## Testing

```sh
sudo su - kafka
bash
/data/kafka/kafka/bin/kafka-topics.sh --create --topic test-topic6 --bootstrap-server 172.20.11:9092,172.20.12:9092,172.20.13:9092 --replication-factor 3 --partitions 3

/data/kafka/kafka/bin/kafka-console-producer.sh --broker-list 172.20.11:9092 --producer.config /data/kafka/kafka/config/producer.properties --topic test-topic6

/data/kafka/kafka/bin/kafka-console-consumer.sh --bootstrap-server 172.20.11:9092,172.20.12:9092,172.20.13:9092 --topic test-topic6 --from-beginning

