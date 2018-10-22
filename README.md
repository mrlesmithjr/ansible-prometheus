# ansible-prometheus

<!-- TOC -->

- [ansible-prometheus](#ansible-prometheus)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- /TOC -->

An [Ansible](https://www.ansible.com) role to install/configure [Prometheus](https://prometheus.io/)

## Requirements

None

## Role Variables

[defaults/main.yml](defaults/main.yml)

## Dependencies

None

## Example Playbook

```yaml
- hosts: monitoring_server
  vars:
    pri_domain_name: "test.vagrant.local"
    prometheus_config:
      global:
        scrape_interval: 1m
        scrape_timeout: 10s
        evaluation_interval: 1m
      ? rule_files
      scrape_configs:
        - job_name: "node"
          static_configs:
            - targets:
                - "127.0.0.1:9100"
              labels:
                host: "node0"
            - targets:
                - "192.168.250.11:9100"
              labels:
                host: "node1"
            - targets:
                - "192.168.250.12:9100"
              labels:
                host: "node2"
        - job_name: "containers"
          static_configs:
            - targets:
                - "192.168.250.11:8080"
              labels:
                docker_host: "node1"
            - targets:
                - "192.168.250.12:8080"
              labels:
                docker_host: "node2"
  roles:
    - role: ansible-prometheus
    - role: ansible-grafana
```

## License

MIT

## Author Information

Larry Smith Jr.

- [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
- [@mrlesmithjr](https://twitter.com/mrlesmithjr)
- [mrlesmithjr@gmail.com](mailto:mrlesmithjr@gmail.com)
