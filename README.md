# k8s
REQUIREMENTS
1. docker desktop, start kubernetes

DOCUMENTATION
1. https://kubernetes.io/docs/home/

WHAT IS K8S
1. kubernets is container orchestration, it will manage creation, deletion, multi-container, and other work related to managing container system


NOTES
1. .yml consist of manifest (API object of k8s)
2. each manifest must consist of four parts
    apiVersion
    kind
    metadata
    spec

TERMINOLOGY
1. Node: Single server in kubernetes cluster
2. Kubelet: kubernetes agent running on nodes
3. Control Plane: Set of containers that manage the cluster, admin containers, sometimes called master
4. Pod: single smallest unit in k8s
5. Service: network endpoint to connect to a pod
6. Imperative Management: approach to manage container in k8s by using command line directly to give command
7. Declarative Management: mainly using .yml file to manage k8s, every management action is contained in .yml file


K8S OBJECT (from high level to low)
1. deployment
2. replicaset
3. service: a stable address for pods, it an object to connect to pod
    ClusterIP: default service
        single, internal
        only reacheable from within cluster (nodes and pods)
        pods can reach service on app port number
    NodePort: 
        it is needed when we want to communicate from outside cluster
        can't used high port (such as 80, the lower the better)
    LoadBalancer:
        for load balancing from outside cluster
        it will spin up ClusterIP and NodePort
    ExternalName:
        seldomly used
    Ingress:
        specific for http traffic

    level of service from high to low
        LoadBalancer
        NodePort
        ClusterIP
    each service with high level will create each service below it, so LoadBalancer will create NodePort, and NodePort will create ClusterIP
4. pod
5. job

USEFULL COMMAND:
1. kubectl run "pod name" --image "image"
2. kubectl create deployment "name" --image "image"
3. kubectl apply -f filename.yml (-f https://url/to/file.yml)
4. kubectl version
5. kubectl get all/pods (-w monitor real time)
6. kubectl scale deployment/"name" --replicas="num"
7. kubectl logs deployment
8. kubectl logs -l run="name"
9. kubectl describe
10. kubectl expose deployment/"name" --port "port" --name "name of service" --type NodePort
11. kubectl create deployment "name of deployment" --image="image" --dry-run=client -o yaml : inspect yaml equivalent for this syntax
12. kubectl api-resource: check kind of k8s object
13. kubectl api-versions: check apiVersion of k8s object
14. kubectl explain "object's kind" --recursive : get .yml file config that maybe usefull