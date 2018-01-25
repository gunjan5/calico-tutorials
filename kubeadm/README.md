## Kubernetes + Calico in 5 minutes with Kubeadm 

Steps:

1. Bring up the VMs: `vagrant up` (This will configure the VMs with correct network interfaces, download and install calicoctl, kubelet, lubectl, kubernetes-cni, loopback CNI, etc.)
2. Login as root to run kubeadm commands: `sudo su`
3. Bring up the kubernetes control plane using kubeadm: `kubeadm init --apiserver-advertise-address=10.96.0.101 --pod-network-cidr=192.168.0.0/16`
4. (optional) Join another non-master node into the k8s cluster: `kubectl join --token=<some.token> 10.96.0.101:6443 --discovery-token-ca-cert-hash sha256:<hash>` (on `node-02`)
5. Run the following commands to configure kubectl to talk to the API server:
 ```bash
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```
6. Apply the Calico manifest for inter-pod networking and NetworkPolicy: `kubectl apply -f https://docs.projectcalico.org/master/getting-started/kubernetes/installation/hosted/kubeadm/1.7/calico.yaml`
7. If it's a single node setup/sandbox then run the following command to allow scheduling pods on master node:
`kubectl taint nodes --all node-role.kubernetes.io/master-`
8. Wait for all the pods to be in `Running` state: `watch kubectl get pods -o wide --all-namespaces`

Kubeadm getting started guide: https://kubernetes.io/docs/getting-started-guides/kubeadm/
