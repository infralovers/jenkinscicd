# Jenkins Docker

## build it

```bash
docker build -t infralovers/jenkins-cicd:latest .
```

## Run it

```bash
docker run -d \
  -p 8888:8080 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name jenkins-cicd \
  infralovers/jenkins-cicd:latest
```

```bash
docker exec -it jenkins-cicd bash
ls -al /var/run/docker.sock
```

## Update Plugin list

To generate a new `plugins.txt` run the following:

```bash
USER='<your user>'
PASSWORD='<your_password>'
JENKINS_HOST=${USER}:${PASSWORD}@localhost:9090
curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/'
```