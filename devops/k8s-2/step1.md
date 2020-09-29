

Launch the **Kubernetes** environment.

```
launch.sh
```{{execute}}

Create a deployment, name should be **titan** and image name **nginx:alpine**. Expose it to externally and scale it to 3.

```
kubectl create deployment titan --image=nginx:alpine
```{{execute}}


```
kubectl scale deployment titan --replicas=3
```{{execute}}

