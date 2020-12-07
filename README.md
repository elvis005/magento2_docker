## Docker image for Magento 2.4.x
Magento 2.4.x has been available for a while and I created the images during the setup of my Magento 2.4.x instance. It took some time and it's better to share for easier onboard for others!

## Multiple containers approach
This repo provides Docker images for Magento 2.4.x versions. It follows the philosophy that one container runs one task. There are 6 containers for production deployment:

1. Nginx
2. PHP (7.4)
3. Cron (7.4)
4. Redis
5. Zookeeper
6. Elasticsearch (7.10.0)

If you use this repo to setup development enviroment, the first 2 containers will be enough. 

It is for production deployment, therefore you may notice there is no MySQL image above. Please use remote database for production instance.

## Quick start

```
git clone https://github.com/elvis005/magento2_docker
cd magento2_docker
mkdir magento2
//download the magento 2.4.x source code to the magento2 folder
docker-compose up -d
```

## Install Magento

After the docker images created, go to Cron container to use command line to setup Magento 2. The details of command line installment guide can be found here: https://devdocs.magento.com/guides/v2.4/install-gde/install/cli/install-cli-subcommands.html