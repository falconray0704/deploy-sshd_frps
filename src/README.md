# 1. Configure of frps serving for bookstack in LAN

## 1.1 Specify following variables in `.env` file for your domain.

```bash
## frps listen port, if you use another one, you must make "bind_port" as the same in frps.ini .
FRPS_BIND_PORT=7100

## sshd port range, frps can serve multi frpc-sshd in LAN
SSHD_PORT_START=7101
SSHD_PORT_END=7110

## Parent path for deployment
#INSTALL_ROOT_PATH=/opt/servers
INSTALL_ROOT_PATH=${HOME}/servers

## Directory for deployment at INSTALL_ROOT_PATH
SERVER_NAME=sshd_frps

INSTALL_PATH=$INSTALL_ROOT_PATH/$SERVER_NAME

## Configuration files for frps
CFGS_DIR=cfgs



# Selfsigned certificates parameters for `1_init.sh`

## Location for selfsigned certificate creation.
SELFSIGNED_CERTS_DIR='selfsigned_rootCA'

## Server domain for CA, here is same as FRPS_SERVER_DOMAIN for selfsigned certificates.
CA_SERVER_DOMAIN='domain.com'

## Server domain for frps deployment.
FRPS_SERVER_DOMAIN='domain.com'

## Server ip for frps deployment.
FRPS_SERVER_IP='192.168.0.1'
```


## 1.2 Specify following variables in `cfgs/frps.ini` file for your domain.
Just refer to official document.
The most required variables are:

* `token` : token for authentication between frpc and frps.
* `subdomain_host` : subdomain for frps routing.


# 2. Initialize services environment

Run the following script to generate selfsigned certificates for frps and frpc.

```bash
./1_init.sh
```

# 3. Launch:

```bash
docker compose up -d
```

