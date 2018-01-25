## Kubernetes + Calico in 5 minutes with Kubeadm 

Steps:

1. `vagrant up`
2. `sudo su`
3. `kubeadm init --apiserver-advertise-address=10.96.0.101 --pod-network-cidr=192.168.0.0/16`
4. (optional) `kubectl join --token=<some.token> 10.96.0.101:6443 --discovery-token-ca-cert-hash sha256:<hash>` (on `node-02`)
5. Run the following commands to configure kubectl to talk to the API server:
 ```bash
   mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```
6. `kubectl apply -f https://docs.projectcalico.org/master/getting-started/kubernetes/installation/hosted/kubeadm/1.7/calico.yaml`
7. `watch kubectl get pods -o wide --all-namespaces`

Kubeadm getting started guide: https://kubernetes.io/docs/getting-started-guides/kubeadm/
