Thanks to Juniarto Samsudin for his post (https://juniarto-samsudin.medium.com/ip-address-changes-in-kubernetes-master-node-11527b867e88)
If host with role master node receive new private IP address, cluster is corrupted.
The solution for this issue here:

# systemctl stop kubelet docker

# cd /etc/

# mv kubernetes kubernetes-backup
# mv /var/lib/kubelet /var/lib/kubelet-backup

# mkdir -p kubernetes
# cp -r kubernetes-backup/pki kubernetes
# rm kubernetes/pki/{apiserver.*,etcd/peer.*}

# systemctl start docker

# kubeadm init --ignore-preflight-errors=DirAvailable--var-lib-etcd

#cp kubernetes/admin.conf ~/.kube/config
