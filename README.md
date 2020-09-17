# project-pw

PS1=‘%n %1~ $’ 

curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

nano ~/.aws/credentials

1. use CTRL + Shift + 6 to mark the beginning of your block.
2. move cursor with arrow keys to end of your block, the text will be highlighted.
3. use CTRL + K to cut/delete block.

aws s3 ls

cd Desktop/Projekt
mkdir raw_data
aws s3 sync s3://deutsche-boerse-xetra-pds/2020-05-25 raw_data/2020-05-25 --no-sign-request
aws s3 sync s3://deutsche-boerse-xetra-pds/2020-05-26 raw_data/2020-05-26 --no-sign-request 
aws s3 sync s3://deutsche-boerse-xetra-pds/2020-05-27 raw_data/2020-05-27 --no-sign-request

aws s3api create-bucket --bucket pnowicki-xetra-data --region us-east-1

aws s3 sync raw_data/2020-05-27 s3://pnowicki-xetra-data/2020-05-27
aws s3 sync raw_data/2020-05-26 s3://pnowicki-xetra-data/2020-05-26
aws s3 sync raw_data/2020-05-25 s3://pnowicki-xetra-data/2020-05-25

DOCKER: 
docker ps 
docker-compose -f nifi-kafka-cluster-pyspark.yml up
docker exec -it projekt_kafka-1_1 bin/bash 

KAFKA:
docker exec -it projekt_kafka-1_1 bin/bash 
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --list
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --create --topic CommonStocks --partitions 3 --replication-factor 3
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --create --topic ETF --partitions 2 --replication-factor 3
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --create --topic ETC --partitions 2 --replication-factor 2
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --create --topic ETN  
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --topic CommonStocks,ETF,ETN,ETC --describe
kafka-topics --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --delete --topic CommonStocks,ETF,ETN,ETC  

kafka-console-producer --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --topic a
kafka-console-consumer --bootstrap-server kafka-1:19091,kafka-2:29091,kafka-3:39091 --topic a

JUPYTER:
docker cp projekt_pyspark-notebook_1:/home/jovyan  project-kafka-streamming   
docker cp  project-kafka-streamming projekt_pyspark-notebook_1:/home/jovyan 


docker exec -u 0 -it 1efb572aa0c9 bash
apt-get update
apt-get install -y package-bar


