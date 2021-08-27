# Mongodb-k8s

I make this repository to learn how to deploy mongodb replicaset in kubernetes cluster, i hope this repository is helpful for others who are looking to deploy mongodb replicaset in kubernetes cluster

## Prerequisite
1. You need nfs server to make dynamic persistent volume(you can use other storage drivers like GlusterFS,Ceph RBD,OpenStack Cinder,and etc.)
2. Deploy the nfs provisioner to your kubernetes cluster
3. Deploy the StateFulSet of mongodb(include headless service)
4. Enjoy it!

**How to run:**
```
$ kubectl create -f mongo.yaml
```
**Access your pod:**
```
$ kubectl exec -it mongo-0 -- mongo
```
I used [Mongo Sidecar](https://github.com/morphy2k/k8s-mongo-sidecar) from [Markus Wiegand](https://github.com/morphy2k) for automate the replicaset initiate inside of the pod

**So The result is like this:**
```
MongoDB shell version v5.0.2
---
rs0:PRIMARY>rs.status()
-----------
"members" : [
		{
			"_id" : 0,
			"name" : "mongo-0.mongo.default.svc.cluster.local:27017",
			"health" : 1,
			"state" : 1,
			"stateStr" : "PRIMARY",
		{
			"_id" : 1,
			"name" : "mongo-1.mongo.default.svc.cluster.local:27017",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
		{
			"_id" : 2,
			"name" : "mongo-2.mongo.default.svc.cluster.local:27017",
			"health" : 1,
			"state" : 2,
			"stateStr" : "SECONDARY",
```
Thanks to [Venkat Nagappan](https://github.com/justmeandopensource), [Francesco Di Franco
](https://github.com/cicciodifranco) for the references and ideas
