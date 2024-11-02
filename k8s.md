# Kubernetes

## Setup Environment using vagrant

use vagrant to setup environment using ubuntu 22.04

```ruby
Vagrant.configure("2") do |config|
  (1..3).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.box = "generic/ubuntu2204"
      node.vm.hostname = "node#{i}"
      node.vm.network "public_network"
    end
  end

  config.vm.provider "hyperv" do |hv|
    hv.memory = "1024"
  end
end
```

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

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.14.2
          ports:
            - containerPort: 80
```

- .spec.replicas: 배포할 복제본 수
- .spec.selector: 배포할 Pod 선택
- .spec.template.metadata.labels: Pod 라벨

## Cluster Configuration

swap 비활성화 해야됨

containerd 사용

#### Pod 간의 통신이 가능하도록 설정

iptables이 트래픽을 filter 할수 있도록 활성화 해줌.

이는 Container 간의 통신을 위해 필요함.

```conf
# /etc/modules-load.d/kubernetes.conf
br_netfilter
```

```conf
# /etc/sysctl.d/99-kubernetes.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
```

### 패키지 설치

```
kubelet kubeadm kubectl
```

### 초기화

```sh
kubeadm config images pull
```

### Cluster 생성

```sh
kubadm init --pod-network-cidr=10.10.0.0/16
```

네트워크 대역을 10.10.0.0/16으로 설정하는 이유는 네트워크 충돌을 피하기 위함.

<!-- kubeadm join 192.168.0.26:6443 --token 8l8yhq.vrf31tts2gm0wxyo \
        --discovery-token-ca-cert-hash sha256:757869f0898ac82b2490fab2d23f535d334fe86e2f9e42474490e434212d82f3 -->

### CNI (Container Network Interface)

Pod 간의 통신을 위해 필요함.

CNI 종류

- Flannel
- Calico
- Weave Net

간단한 Calico 를 쓰겠음

```sh
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### ERROR

kube-proxy 에러

```sh
containerd config default | tee /etc/containerd/config.toml
sed -i 's/SystemdCgroup = false/SystemdCgroup = true/g' /etc/containerd/config.toml
systemctl restart containerd
systemctl restart kubelet
```
