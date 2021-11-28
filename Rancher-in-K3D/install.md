```ShellSession
# Follow steps below once you already installed K3D

k3d cluster create k3drancher --api-port 127.0.0.1:6445 --port '80:80@loadbalancher' --servers 3 --agents 3

kubectl cluster-info

kubeclt get services --all-namespaces

# apply cert-manager
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.5.4/cert-manager.yaml

kubectl create namespace cattle-system

# you may run 'K9S' to see which pods are running

# install Rancher
helm install rancher rancher-latest/rancher \
--namespace cattle-system --version 2.6.0 \
--set hostname=myrancher.com

kubectl -n cattle-system rollout status deploy/rancher

# go to browser, enter URL - https://myrancher.com
# copy kubectl from Web UI, run it to get bootstrap password
# go back to terminal, paste from clipboard, run & copy bootstrap password 
# go back to the browser, and paste your password to sign in
```
