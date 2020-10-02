

Launch the **Kubernetes** environment.

```
launch.sh
```{{execute}}

Create a Pod, name should be **jenkins** and image name **jenkins**.

```
kubectl run jenkins-demo --image=jenkins 
```{{execute}}


```
kubectl expose pod jenkins-demo --name jenkins-service --port 8080 --type NodePort
```{{execute}}

Run the jenkins file

```
cat << EOF > /root/jenkins.yaml
kind: Pod
apiVersion: v1
metadata:
  name: jenkins
  labels:
    app: jenkins
spec:
  volumes:
    - name: data
      emptyDir:
        medium: Memory
        sizeLimit: 1.5Gi
  containers:
    - name: jenkins
      image: jenkins
      workingDir: /var/jenkins_home
      ports:
        - containerPort: 8080
          name: test-1
        - containerPort: 50000
          name: test-2
      securityContext:
        runAsUser: 1000
        runAsGroup: 1000
      volumeMounts:
        - name: data
          mountPath: /var/jenkins_home/
EOF
```{{execute}}


```
kubectl create -f /root/jenkins.yaml
```{{execute}}

Service for **Jenkins Pod**

```
kind: Service
apiVersion: v1
metadata:
  name: jenkins-svc
spec:
  type: NodePort
  ports:
    - name: test-1
      port: 8080
      targetPort: 8080
      nodePort: 32500
    - name: test-2
      port: 50000
      targetPort: 50000
      nodePort: 31500
  selector:
    app: jenkins
```{{execute}}




