### Multus

Please refer to [Multus Quickstart Installation Guide](https://github.com/intel/multus-cni#quickstart-installation-guide) to install Multus.

Or follow the instructions
```
kubectl apply -f multus-daemonset-pre-1.16.yml
```

If using v1.16 or higher
```
kubectl apply -f multus-daemonset.yml
```

## OpenvSwitch
```
sudo apt update && sudo apt install openvswitch-switch -y
ovs-vsctl add-br br1
```

## OVS-CNI
```
cd example/
kubectl apply -f ovs-cni-pre-1.16.yaml
```
If using v1.16 or higher
```
cd example/
kubectl apply -f ovs-cni.yaml
```
Create a NetworkAttachmentDefinition
```
cat <<EOF >./ovs-net-crd.yaml
apiVersion: "k8s.cni.cncf.io/v1"
kind: NetworkAttachmentDefinition
metadata:
  name: ovs-net
  annotations:
    k8s.v1.cni.cncf.io/resourceName: ovs-cni.network.kubevirt.io/br1
spec:
  config: '{
      "cniVersion": "0.3.1",
      "type": "ovs",
      "bridge": "br1"
    }'
EOF
kubectl apply -f ovs-net-crd.yaml
```
CNI Network Controller
```
cd example/
kubectl apply -f unix-daemonset.yaml
```
## Test

ubuntu-test.yaml
```
cd example/
kubectl apply -f ubuntu-test.yaml
```
