# Infra
infrastracture repo
## Homework 5
#### 1. How to connect internalhost through bastion

```bash
* ssh 10.132.0.3 -o ProxyCommand="ssh -W %h:%p 35.205.76.161"
* ssh 10.132.0.3 -o ProxyCommand="ssh 35.205.76.161 nc %h %p 2> /dev/null"
* ssh -J 35.205.76.161 10.132.0.3
```
Using .ssh/config
```
Host *
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_rsa
    UseKeychain yes
    ServerAliveInterval 30

host bastion
    hostname 35.205.76.161

host internalhost
    hostname 10.132.0.3
    proxyjump bastion
```
Another examples
```
host internalhost
    hostname 10.132.0.3
    ProxyCommand ssh -W %h:%p bastion

host internalhost
    hostname 10.132.0.3
    ProxyCommand ssh bastion nc %h %p 2> /dev/null
```
#### 2. Host configuration.
```bash
Хост bastion, внешний IP: 35.205.76.161, внутренний IP: 10.132.0.2
Хост: internalhost, внутренний IP: 10.132.0.3
```
## Homework 6
All scripts is placed in folder config-scripts
#### Manual install:
* Install Ruby `config-scripts/install_ruby.sh`
* Install MongoDB `config-scripts/install_mongodb.sh`
* Deploy App `config-scripts/deploy.sh`

#### Auto install through [Google Cloud Platform](https://cloud.google.com/)
use this command to install app via google cli from local machine's file:
```bash
gcloud compute instances create reddit-app \
  --boot-disk-size=10GB \
  --image-family ubuntu-1604-lts \
  --image-project=ubuntu-os-cloud \
  --machine-type=g1-small \
  --tags puma-server \
  --restart-on-failure \
  --zone=europe-west1-d \
  --metadata-from-file startup-script=config-scripts/startup-script.sh
```
use this command to install app via google cli from passed through command (from uri change option --metadata on --metadata-from-uri):
```bash
gcloud compute instance create reddit-app \
  --boot-disk-size=10GB \
  --image=ubuntu-1604-xenial-v20170815a \
  --image-project=ubuntu-os-cloud \
  --tags http-server \
  --machine-type=f1-micro \
  --restart-on-failure \
  --metadata startup-script='wget -O - \  https://gist.githubusercontent.com/spybond08/c063f6c12ff852d82163deadbc09fcbd/raw/2e2cde1f8698058ee726d3d0549666e55f0b6988/gistfile1.txt | bash'
```  
