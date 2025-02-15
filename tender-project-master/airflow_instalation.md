## Apache Airflow instalation
Airflow will be running on a vortual machine from Docker container. 
Docker file is build using apache/airflow:2.2.3 as a base image, adding neccesary dependancies and modules to run DAGs

```
apache-airflow-providers-google
apache-airflow-providers-http
pyarrow
pandas
sqlalchemy
psycopg2-binary
pyspark
```

Dockerfile is created with all needed modules and dependancies and Google sdk.
Official Apache Airflow [docker-compose.yaml](https://airflow.apache.org/docs/apache-airflow/stable/docker-compose.yaml) file will be used, replacing Google project attributes with ones used in this particular project. 

From an Airflow folder, containing Dockerfiles, run:

```
docker-compose build
```

Initialise Airlow databases:

```
docker-compose up airflow-init
```

Initialise user in .env file with:

```
echo -e "AIRFLOW_UID=$(id -u)" > .env
```

Running airflow-init also creates all neccesary directories for Airflow operation like dags, logs, plugins.
Running Airflow on VM requires port forward.

Airflow interface is available on [localhost:8080](http://localhost:8080/home)


# How to SSH

gcloud compute os-login ssh-keys add \
    --key-file='/Users/reneboygarcia/Documents/Capstone Peer Review/DataEngineering/tender-project-master/terraform/GOOGLE_APPLICATION_CREDENTIALS.json' \
    --project=eu-pub-tender-de-2023 \
    --ttl=15d
    
# How to get external IP

`curl ifconfig.me`

# Port Forward
gcloud compute firewall-rules create airflow-web-ui --allow tcp:8080

