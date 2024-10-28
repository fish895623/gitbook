# Teraform

Terraform은 HashiCorp에서 만든 오픈 소스 IaC인프라 코드 소프트웨어 도구이다. HCL, JSON으로 데이터 센터 인프라를 정의하고 프로비저닝할 수 있다.

### Key Concepts

1. **Providers**: Providers are responsible for understanding API interactions and exposing resources. They are a logical abstraction of an upstream API.
2. **Resources**: Resources are the most important element in the Terraform language. Each resource block describes one or more infrastructure objects, such as virtual networks, compute instances, or higher-level components such as DNS records.
3. **Modules**: Modules are containers for multiple resources that are used together. A module consists of a collection of .tf files in a directory.
4. **State**: Terraform uses state to map real-world resources to your configuration, keep track of metadata, and improve performance for large infrastructures.
