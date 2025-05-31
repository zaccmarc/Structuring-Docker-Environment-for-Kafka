# Structuring-Docker-Environment-for-Kafka
Structuring Docker Environment for Kafka

# DOCKER TO KAFKA DEVELOPMENT

Date: May 31, 2025

## Structuring Docker Environment for Kafka, and performing some exercises

I'm going to set up my Kafka environment and do some exercises to complete my study on this topic.

Some features are enabled because I had already downloaded and run some images such as MongoDB and Kafka itself on Docker Desktop, but due to the necessary RAM resources I chose to migrate to Docker Engine.

I'm preparing this environment to develop a real-time data processing and analysis project with python, but for now we're going to stick with just creating the environment.

## Structuring Docker Engine in WSL2

I chose to use Docker Engine in WSL2 over Docker Desktop because of its ability to only consume the minimum amount of memory needed to run the Docker Daemon. Unlike Docker Desktop, which consumed about 3GB of RAM even without loading any images.

And because of its performance it is even greater than that of Docker Desktop, due to its execution directly inside the WSL2 instance itself, eliminating the need for a separate Linux instance.

## Installing WSL

First I enabled the Virtual Machine Platform with the following commands

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestar
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestartt
```

Download do WSL2

```
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
```

Set WSL2 as default when installing a new Linux distribution in Power Shell as the administrator

```
wsl --set-default-version 2
```

I installed the Linux distribution Ubuntu 20.04 LTS

## Installing Docker with Docker Engine (Docker Native)

### installing prerequisites

```
sudo apt update && sudo apt upgrad
sudo apt remove docker docker-engine docker.io containerd runc
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg\
    lsb-releasee
```

### Adding Docker Repository to Ubuntu Source List

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

### Installing the Docker Engine

```
sudo apt-get update
```

---

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

### Configuring Kafka

I created the Kafka directory and inserted the docker-compose.yml file

Install docker-compose:

```
Docker-compose: https://docs.docker.com/compose/install/
```

I initialized the Kafka cluster through docker-compose:

```
docker compose up -d
```

[](https://media.licdn.com/dms/image/v2/D4D12AQFCUFcPEq5WOw/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1684884064847?e=1753920000&v=beta&t=XlftRqa4TE18rLCy2Ifew65VuKzeOXOnskM67IwVXu4)

[](https://media.licdn.com/dms/image/v2/D4D12AQF4atFBm-T77g/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1684884125516?e=1753920000&v=beta&t=IgOiXr3SaZRfUnRkKi2rUpoDhQyyjN9rdGKfdamRnHs)

I accessed Confluent through localhost :

```
http://localhost:9021
```

## Performing Tests

I accessed confluent (Localhost), to perform some tests, I'm going to create a KSQL stream and check if everything is ok, I had already done some tests before when using Docker Desktop:

[](https://media.licdn.com/dms/image/v2/D4D12AQGuco1MJSa-Xg/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1684884520785?e=1753920000&v=beta&t=asOv8UV-L6jjzidgm1cxEMkGjyRYsnJ3XigEVlwqnBQ)

### 1. Creating the msg_usuario_csv topic:

```
CREATE STREAM msg_usuario_csv (id INT, nome VARCHAR ) WITH (kafka_topic='msg_usuario_csv', PARTITIONS=2, REPLICAS=1, value_format='DELIMITED');
```

[](https://media.licdn.com/dms/image/v2/D4D12AQGC9pnZOWaOKg/article-inline_image-shrink_1500_2232/article-inline_image-shrink_1500_2232/0/1684886570591?e=1753920000&v=beta&t=H9GBT-7d8sx1FTuLXbagSgV6QiTRts_GOW1GighKTl0)

After the steps taken, the environment was successfully structured! I hope you enjoyed! Soon I'm thinking of bringing more articles continuing the data stream, to later Process and analyze data in real time with Kafka and Python, today I just set up this environment, so... Wait!
