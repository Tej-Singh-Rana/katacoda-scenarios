

Launch the **Kubernetes** environment.

```
launch.sh
```{{execute}}

Create a Pod, name should be **jenkins** and image name **jenkins**.

```
kubectl run jenkins --image=jenkins 
```{{execute}}


```
kubectl expose pod jenkins --name jenkins-service --port 8080 --type NodePort
```{{execute}}

Run the jenkins file

```
cat << EOF > /root/jenkins.yaml
kind: Pod
apiVersion: v1
metadata:
  name: jenkins
  labels:
     run: jenkins
spec:
  volumes:
  - name: data
    hostPath:
      path: /opt/data
      type: DirectoryOrCreate
  containers:
  - name: jenkins
    image: jenkins
    volumeMounts:
    - name: data
      mountPath: /var/jenkins_home
EOF
```{{execute}}


```
kubectl create -f /root/jenkins.yaml
```{{execute}}





