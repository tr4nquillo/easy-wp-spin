# Easy Local Wordpress instance with docker-compose

## Purpose 

The purpose of this setup is to enable an easy spin-up of a wordpress instance with the latest version of Wodpress and Mysql images.

## Prerequisities 

- **docker** and **docker compose** should be installed. 
- container environments are: set either through defining environment variables or by creating .env file
- to persist the contents of the database and the web root of the web server, in this case apache, use the predefined named volumes.
- in case you want to use custom host directories for the volumes (bind mounts), execute these commands in a directory of your choice to ensure that proper permissions are set:

```
mkdir wp-db-data && \
sudo chown -R 999:999 wp-db-data && \
sudo chcon -Rt svirt_sandbox_file_t /tmp/wp-db-data && \
mkdir wp-www-data && \
sudo chown -R 33:33 wp-www-data && \
sudo chcon -Rt svirt_sandbox_file_t /tmp/wp-www-data

```
- uncomment the lines where the custom volumes are set in *docker-comoose.yaml*
- comment out the lines where the volumes are set with the named volumes 
- after that run docker-compose with this configuration

## Troubleshooting

If you decide to switch from named volumes to bind volumes or vice versa, make sure you've cleaned up previous state properly, ie. executed **docker-compose down**. Otherwise you'll get permission errors on the volumes.

## Advantages of using docker compose for local environments

The advantage of using docker-compose over single containers:
- easier container management - up, down, run, stop, state persistence with volumes etc.
- guarantee order with depends_on
- network is automatically managed
- scaling of services 
- supports environment variables with .env
- containers communicate with container names

## Best practice 

- use .env files to better configure environments

```
# .env file in the same directory as your docker-compose.yaml
MYSQL_ROOT_PASSWORD=MySecretPassword
MYSQL_DATABASE=artshop
MYSQL_USER=art
MYSQL_PASSWORD=ArtOwner
```



- never commit .env files to your repository

