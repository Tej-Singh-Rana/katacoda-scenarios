

Launch the **Kubernetes** environment.

```
launch.sh
```{{execute}}

Create a Pod, name should be **jenkins** and image name **jenkins**.

```
kubectl run jenkins --image=jenkins 
```{{execute}}


```
kubectl expose pod jenkins --name jenkins-service --tcp 8080 
```{{execute}}

