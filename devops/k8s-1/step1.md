
Create a Pod with the imperative command.


launch the kubernetes cluster.

```
launch.sh 
```{{execute}}

Check the status of the nodes.

```
kubectl get nodes 
```{{execute}}


Create a nginx pod, name should be **nginx-test** and image should be **nginx**.


```
kubectl run nginx-test --image=nginx
```{{execute}}


 