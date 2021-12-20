ETCD - Commands (Optional)
(Optional) Additional information about ETCDCTL Utility
ETCDCTL is the CLI tool used to interact with ETCD.
ETCDCTL can interact with ETCD Server using 2 API versions - Version 2 and Version 3.  By default its set to use Version 2. Each version has different sets of commands.
For example ETCDCTL version 2 supports the following commands:
    etcdctl backup
    etcdctl cluster-health
    etcdctl mk
    etcdctl mkdir
    etcdctl set
Whereas the commands are different in version 3
    etcdctl snapshot save 
    etcdctl endpoint health
    etcdctl get
    etcdctl put
To set the right version of API set the environment variable ETCDCTL_API command
export ETCDCTL_API=3
When API version is not set, it is assumed to be set to version 2. And version 3 commands listed above don't work. When API version is set to version 3, 
version 2 commands listed above don't work.
Apart from that, you must also specify path to certificate files so that ETCDCTL can authenticate to the ETCD API Server. The certificate files
are available in the etcd-master at the following path. We discuss more about certificates in the security section of this course. So don't worry if this looks complex:

    --cacert /etc/kubernetes/pki/etcd/ca.crt     
    --cert /etc/kubernetes/pki/etcd/server.crt     
    --key /etc/kubernetes/pki/etcd/server.key
So for the commands I showed in the previous video to work you must specify the ETCDCTL API version and path to certificate files. Below is the final form:

kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / 
            --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt 
              --cert /etc/kubernetes/pki/etcd/server.crt  --key /etc/kubernetes/pki/etcd/server.key" 



kubctl run nginx --image=nginx

kubectl run nginx --dry-run=client --image=nginx -o yaml
Create an NGINX Pod

kubectl run nginx --image=nginx

Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

kubectl run nginx --image=nginx --dry-run=client -o yaml

Create a deployment

kubectl create deployment --image=nginx nginx

Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml

Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

kubectl create -f nginx-deployment.yaml

OR

In k8s version 1.19+, we can specify the --replicas option to create a deployment with 4 replicas.

kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml 
