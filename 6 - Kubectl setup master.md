## Download the `kubectl`.
```
$ curl -O https://storage.googleapis.com/kubernetes-release/release/v1.6.1/bin/linux/amd64/kubectl
```
## Change permission of `kubectl`.
```
$ chmod +x kubectl
```
## Move `kubectl` to `/opt/bin` and add path to executable.

```
$ sudo mkdir -p /opt/bin
$ sudo mv ./kubectl /opt/bin/kubectl
$ PATH="$PATH:/opt/bin/"
```
## Configure the `kubectl context`
Get into to the directory where we have generated the `ca` and `admin` keys. and execute following commands.

```
$ cd /home/core/
```
Configure kubectl to connect to the target cluster using the following commands, replacing several values as indicated:
- Replace 174.138.76.103 in following command with the Public IP address of Master Node.
```
kubectl config set-cluster default-cluster --server=https://174.138.76.103 --certificate-authority=ca.pem
kubectl config set-credentials default-admin --certificate-authority=ca.pem --client-key=admin-key.pem --client-certificate=admin.pem
kubectl config set-context default-system --cluster=default-cluster --user=default-admin
kubectl config use-context default-system
```

# Verify kubectl Configuration and Connection.
```
$ kubectl get nodes
NAME             STATUS                     AGE       VERSION
174.138.76.103   Ready,SchedulingDisabled   15m       v1.6.1+coreos.0
174.138.76.107   Ready                      26m       v1.6.1+coreos.0
174.138.76.108   Ready                      44m       v1.6.1+coreos.0
```
