# Node Exporter - Instalação

Este arquivo tem como instrução a instação do node_exrpoter me servidores linux para captura de métricas com o Prometheus

## 1. Instalação

### 1.1 Download - Versão v1.10.2
```shell
wget [https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz](https://github.com/prometheus/node_exporter/releases/download/v1.10.2/node_exporter-1.10.2.linux-amd64.tar.gz)
```
### 1.2 Extração
```shell
tar xvfz node_exporter-1.10.2.linux-amd64.tar.gz  
```
### 1.3 Mover para bin
```shell
sudo mv node_exporter-1.10.2.linux-amd64/node_exporter /usr/local/bin
```
## 2. Usuário do serviço
#### 2.1 Criar usuário e permissão
```shell
sudo useradd -r -M -s /bin/false node_exporter && sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter  
```

## 3. Serviço

### 3.1 Criar arquivo do serviço
```shell
sudo nano /etc/systemd/system/node_exporter.service
```
### 3.2 Configuração
 ```shell
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter
Restart=on-failure

[Install]
WantedBy=multi-user.target  
````

### 3.3 Recarregar, habilitar e iniciar
```shell
sudo systemctl daemon-reload  && sudo systemctl enable --now node_exporter  && sudo systemctl status node_exporter
```
