Project Instructions

1: Set up a Kubernetes cluster with 5 nodes "1 Master + 4 Worker Nodes".

2: Create 2 namespaces named "test" and "production".

3: Create roles for the group named "junior" to have all rights such as "read, list, create..." on all resources in the "test" namespace and only "read and list" rights on all resources in the "production" namespace and associate them with the group. Likewise, create a role for the group named "senior" to have all rights such as "read, list, create..." on all resources in the "production" and "test" namespaces and only "read and list" rights on other resources in the cluster and associate them with the group.

4: Install an "ingress controller" of your choice (nginx, traefik, haproxy etc.)

5: On the 3 worker nodes you choose in the cluster, only the pods that you will deploy in the "production" environment and created by the cluster can be scheduled. Ensure that other pods are not created on this worker node.

6: Deploy the wordpress application in both "test" and "production" namespaces (created from wordpress:latest and mysql:5.6 images)

 -> mysql will be accessible from within the cluster with a "ClusterIp" type service.
 
 -> Long term data of both applications will be stored on "persistent volumes".
 
 -> Both applications will be scheduled on the same worker node.
 
 -> Cpu and memory resource constraints will be defined for both applications.

7: The wordpress application deployed in the "test" namespace will be exposed to the outside world as "testblog.example.com" and the wordpress application deployed in the "production" namespace will be exposed to the outside world via ingress as "companyblog.example.com".

8: Create a deployment in the "production" namespace from the "ozgurozturknet/k8s:v1" image, with 5 replicas, where 2 pods can be updated at the same time as an update strategy. Define a "liveness probe" that queries the "/healthcheck" endpoint and a "readiness probe" that queries the "/ready" endpoint.

9: Make the deployment you created in the previous task accessible from the outside world with a "loadbalancer" type service.

10: Deploy "fluentd" application as a "daemonset" in the cluster.

11: Deploy a 2 node "mongodb" cluster as a "statefulset" in the cluster. Make sure that the "mongodb" cluster is running.

12: Create a "service account" with "read and list" rights on all objects in the cluster. Create a pod to which you connect this service account and list all pods in the cluster with "curl".


Translated with www.DeepL.com/Translator (free version)
