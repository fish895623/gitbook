---
description: '@Jenkins, Docker, agnet, build'
---

# Pipeline build agent with Docker container

```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post http://%2Fvar%2Frun%2Fdocker.sock/v1.40/images/create?fromImage=alpine&tag=latest: dial unix /var/run/docker.sock: connect: permission denied
```

Jenkins 빌드 도중 docker agent를 이용하였을때 이러한 오류가 뜨게 되면 

Jenkins 내부 root 쉘로 들어가서 아래의 명령어를 실행해 준다.

```bash
usermod -aG docker jenkins
chmod 777 /var/run/docker.sock
```

