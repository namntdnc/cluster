# NOTE
## Connection
### 1. Test connection
    ansible -i host.local local -m ping

## Deploy
### 1. Khởi tạo hệ thống 
    ansible-playbook -i hosts.local -l local provison.yml

## Cluster Up

## Rancher-server
> Sau khi cluster up thi rancher-server moi hoat dong