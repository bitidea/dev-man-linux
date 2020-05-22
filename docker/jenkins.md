# Jenkins

https://github.com/jenkinsci/docker/blob/master/README.md

```bash
docker run -d --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v /docker-data/jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```
