---
title: "Long Page Title"
linkTitle: "Short Nav Title"
weight: 100
description: >-
     Page description for heading and indexes.
---

## Heading

Edit this template to create your new page.

* Give it a good name, ending in `.md` - e.g. `getting-started.md`
* Edit the "front matter" section at the top of the page (weight controls how its ordered amongst other pages in the same directory; lowest number first).
* Add a good commit message at the bottom of the page (<80 characters; use the extended description field for more detail).
* Create a new branch so you can preview your new file and request a review via Pull Request.

1.	Command:- 
k run cache --image lfccncf/redis:3.2 --port 6379 -n web
k get pods  -n web- status should be running


2.	k create secret generic another-secret --from-literal=key1=value4

root@k8s-master:/home/ubuntu# cat nginx-secret.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx-secret
  name: nginx-secret
spec:
  containers:
  - image: nginx
    name: nginx-secret
    env:
    - name: COOL_VARIABLE
      valueFrom:
        secretKeyRef:
          name: another-secret
          key: key1

k apply -f nginx-secret.yaml
k get pods  => should be running


3.	
k run nginx-resources --image nginx -n pod-resources --dry-run=client -o yaml > nginx-resources.yaml
k apply -f nginx-resources.yaml
k get pods -n pod-resources


4.	You are tasked to create a ConfigMap and consume the ConfigMap in a pod using a volume mount.
Solution:- 

k run nginx-configmap --image nginx --dry-run=client -o yaml > nginx-configmap.yaml

root@k8s-master:/home/ubuntu# cat nginx-configmap.yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
  name: nginx-configmap
spec:
  containers:
  - image: nginx
    name: nginx-configmap
    volumeMounts:
    - mountPath: /also/a/path
      name: test-volume
  volumes:
  - name: test-volume
    configMap:
      name: another-config

k apply -f nginx-configmap.yaml
k get pods

5.	Your application’s namespace requires a specific service account to be used.

root@k8s-master:/home/ubuntu# k get sa -n production
NAME                SECRETS   AGE
default             1         2m29s
restrictedservice   1         56s

kubectl set serviceaccount deployment app-a restrictedservice -n production
