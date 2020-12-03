# NOTE

## Require
- vagrant 2.2.10
- virtualbox 6.0

## Prepare sourece
- git clone https://github.com/namntdnc/auto-deploy.git ./source

## Not config  YET
PHP 
NGINX
PHP-FPM USER, GROUP 

## Connection
### 1. Test connection
    ansible -i hosts.local local -m ping

## Deploy
### 1. Khởi tạo hệ thống 
    ansible-playbook -i hosts.local -l local provison.yml

## Cluster Up
    rke up --config cluster.yml
    mkdir -p ~/.kube
    cp ~/ansible-playbook/kube_config_cluster.yml ~/.kube/config


## Rancher-server
> Sau khi cluster up thi rancher-server moi hoat dong

## Synchronize source
ansible-playbook apply-deployment.yml -i hosts.local --extra-vars "_target_source=..."