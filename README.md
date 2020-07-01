### Before you begin
Installing Docker
```
apt-get update
apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
apt-get update && apt-get -y install docker-ce docker-ce-cli containerd.io
```
### Create SSL certificate
```
letsencrypt certonly --standalone -d turn1.bptest.cloud
```
### Edit turnserver/turnserver.cfg according your db selection (mysql or postgresql or redis or mongodb)

```
docker-compose -f docker-compose-all.yml up --build --detach ## for different yaml file
docker-compose up -d
```

Notice: May restart needed for coturn container, if it could not access database yet, due initialization delay.
``` 
docker restart docker_coturn_1
docker-compose -f docker-compose-all.yml down
docker-compose down
```
### Stop with volume removal
```
docker-compose down --volumes
```
