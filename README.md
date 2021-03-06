# docker-hashicorp-nomad
A debian:latest based docker container running HashiCorp's nomad on CoreOS instances.

## From cloud-config
```
#cloud-config

coreos:
  units:
    - name: nomad.service
      command: start
      content: |
        [Unit]
        Description=HashiCorp nomad service
        Documentation=https://www.nomadproject.io/docs/index.html
        [Service]
        Restart=always
        ExecStart=/usr/bin/docker run --rm --name nomad \
          --net=host \
          -v /run/docker.sock:/run/docker.sock \
          -p 4646:4646 \
          -p 4647:4647 \
          -p 4648:4648 \
          godmodelabs/hashicorp-nomad agent -dev
        ExecStop=-/usr/bin/docker stop nomad
```
