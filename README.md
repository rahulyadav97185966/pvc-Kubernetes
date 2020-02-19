# pvc-Kubernetes
# On Server (master)#
apt install nfs-kernel-server : install nfs server
mkdir -p /mnt/sharedfolder
chown nobody:nogroup /mnt/sharedfolder
chmod 777 /mnt/sharedfolder
vim /etc/exports
    |
    /mnt/sharedfolder *(rw,sync,no_root_squash)
exportfs -r
systemctl restart nfs-kernel-server
ip a | less :  to get the ip of server

# On Client (node01) #
apt-get install nfs-common
mount -t nfs 172.17.0.34:/mnt/sharedfolder /mnt  :: put ip of server
df -h
umount /mnt
    
 #now the nfs is set perfectly , now goto master and create pv.yml and pvc and the deployment of pod which you want to run#   
    # we are using wordpress and backend as mysql #
    
    1) create pv using vim pv.yml  : put the code of file pv.yml in this file
    2) in above file put ip address of server and path of the pv
    3) kubectl create -f pv.yml
    4) kubectl get pv
    5) Now create PVC and check
    6) kubectl create -f pvc.yml
    7) kubectl get pvc
    8) kubectl get pv
    8) now create pod-sql.yml
    9) kubectl create -f pod-sql.yml
    10) kubectl get pods
    11) kubectl get pv
    
    (Now to see if the pv-pvc bounded successfully execute the pod and use command 'df -h')
      e.g. kubectl exec -it wordpress-mysql-d88687df4-vnhsn bash
              |
              df -h
              
    (Get pv)
     kubectl get pv
