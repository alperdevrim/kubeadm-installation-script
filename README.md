# Running the Script

To execute the script, follow these steps:

1. Grant execute permissions to the script:
   ```bash
   chmod +x kubeadm.sh
   ```

2. Run the script:
   ```bash
   ./kubeadm.sh
   ```


After running the script, repeat this steps for each control plane and worker nodes to ensure proper configuration.

# Control Plane Node Setup

After running the script in the control plane node, initialize Kubernetes:

```bash
kubeadm init
```

## Configure kubectl Access

To start using your cluster, run the commands below:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

If you are a root user, you can run the following command:

```bash
export KUBECONFIG=/etc/kubernetes/admin.conf
```

## Apply CNI YAML

To set up the container network interface (CNI), apply the following YAML:

```bash
kubectl apply -f https://reweave.azurewebsites.net/k8s/v1.30/net.yaml
```

## Join Worker Nodes

To join worker nodes to the cluster, run  the `kubeadm join` command  displayed on the control plane node after initialization. The command will look similar to the following:

```bash
kubeadm join <control-plane-host>:<port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```
Run this command for each worker nodes.

Ensure you copy and run the exact command shown in your terminal output during the `kubeadm init` process.
