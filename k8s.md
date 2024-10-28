# Kubernetes

## Pod

하나이상의 컨테이너로 구성되어 있음

### Volume

```yaml
.spec.volumes
```

1. emptyDir
1. fc (fiber Channel)
1. hostPath
1. nfs
1. secret

## Service

Pod 에 대한 진입점을 제공

### ClusterIp

### NodePort

Pod 에 대해 포트를 열어줌

### LoadBalancer

Pod 에 트래픽을 분산시켜줌

### ExternalName

단순하게 DNS 역할만 수행

## ReplicaSet

동일한 Pod의 여러 복제본을 보장하는데 사용됨.

High Availability / FailOver

특정 수의 Pod가 항상 실행되도록 함.

## Deployment
