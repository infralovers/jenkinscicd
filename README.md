# Jenkins Docker

## build it

```bash
docker build -t infralover/jenkins-cicd:latest .
```

## Run it


```bash
docker run -d \
  -p 8888:8080 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --name jenkins-cicd \
  --network mynetwork \
  infralover/jenkins-cicd:latest
```

## Update Plugin list

```bash
JENKINS_HOST=admin:9373059862464689b4b9566932a2f3c6@localhost:9090
curl -sSL "http://$JENKINS_HOST/pluginManager/api/xml?depth=1&xpath=/*/*/shortName|/*/*/version&wrapper=plugins" | perl -pe 's/.*?<shortName>([\w-]+).*?<version>([^<]+)()(<\/\w+>)+/\1 \2\n/g'|sed 's/ /:/'
```