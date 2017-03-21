## Kubernetes + Calico in 5 minutes with Kubeadm 

Steps:

1. vagrant up
2. sudo su
3. kubeadm init --api-advertise-addresses=10.96.0.101
4. kubectl join (on `node-02`)
5. kubectl apply -f http://docs.projectcalico.org/v2.1/getting-started/kubernetes/installation/hosted/kubeadm/calico.yaml
6. kubectl get pods -o wide --all-namespaces

Kubeadm getting started guide: https://kubernetes.io/docs/getting-started-guides/kubeadm/
