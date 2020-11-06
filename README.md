# NOTE

## Require
- vagrant 2.2.10
- virtualbox 6.0

## Prepare sourece
- git clone https://github.com/namntdnc/auto-deploy.git ./source

## Not config 
PHP 
NGINX

## Connection
### 1. Test connection
    ansible -i hosts.local local -m ping

## Deploy
### 1. Khởi tạo hệ thống 
    ansible-playbook -i hosts.local -l local provison.yml

## Cluster Up

## Rancher-server
> Sau khi cluster up thi rancher-server moi hoat dong