<!-- TOC -->

- [The Elastic Stack](#the-elastic-stack)
  - [Setup](#setup)

<!-- /TOC -->


# The Elastic Stack

## Setup

1. Clone the this repository:

```bash
git clone https://github.com/mpolinowski/elk-server-compose,git
```

2. Build and Run:

```bash
docker-compose build
docker-compose up
```

3. Create Random User Logins

Now I can connect to the running Elasticsearch container and generate random passwords for both the `elastic` and `kibana_system` user:


```bash
docker-compose exec -T elasticsearch bin/elasticsearch-reset-password --batch --user elastic
```


```bash
docker-compose exec -T elasticsearch bin/elasticsearch-reset-password --batch --user kibana_system
```


4. Replace Kibana User Login

Replace the password of the `kibana_system` user inside the Kibana configuration file with the password generated in the previous step:


_kibana/config/kibana.yml_


```yml
elasticsearch.username: kibana_system
elasticsearch.password: 'mygeneratedpassword'
```


And change the __ELASTIC_PASSWORD__ environment variable from the elasticsearch service inside the Compose file `docker-compose.yml`.:


```yml
ELASTIC_PASSWORD: 'mygeneratedpassword'
```

5. Restart and Start Using Elasticsearch / Kibana