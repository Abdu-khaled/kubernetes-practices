# kubernetes-practices

## Part1:

### 1. Create pod nginx with name my nginx direct from command don't use yaml file.

**Explanation:**
 - To create pod nginx without yaml file we use imperative way by use `kubectl run`. 
**Command:**
```bash
kubectl run my-nginx --image nginx
kubectl get pods
```
 - my-nginx: the pod name 
 - --image=nginx : tells Kubernetes to use the official nginx image

**Verification Command:**  
![](./screenshot/01.png)

---

### 2. Create pod nginx with name my nginx command and use Image nginx123  direct from command don't use yaml file.

**Explanation:**
 - To create pod nginx without yaml file we use imperative way by use `kubectl run`. 
**Command:**
```bash
kubectl run my-nginx --image nginx123
kubectl get pods
```

**Verification Command:**  
![](./screenshot/02.png)

---

### 3.  Check the status and why it doesn't work.


**Explanation:**
 - The Pod is created but cannot run because the image nginx123 does not exist in Docker Hub (or your configured registry). Kubernetes will try to pull it, fail, and mark the Pod as ImagePullBackOff.
   
**Command:**
```bash
kubectl get pods
kubectl describe pod my-nginx
```
**Verification Command:**  
![](./screenshot/03.png)


---

### 4. I need to know node name - IP - Image Of the POD.

**Explanation:**
  - we can use `kubectl get pod -o wide` to see the node name and Pod IP.
  - To check which image the pod using, we use `kubectl describe pod`.

**Command:**
```bash
kubectl get pod my-nginx -o wide
kubectl describe pod my-nginx | grep -i image
```
**Verification Command:**  
![](./screenshot/04.png)

---

### 5.  Delete the pod. 

**Explanation:**
  - we can use `kubectl delete pod` for delete andy pod.

**Command:**
```bash
kubectl delete pod my-nginx
```

**Verification Command:**  
![](./screenshot/05.png)

---

### 6. Create another one with yaml file and use label.

**Explanation:**
  - Now we will use Declarative way by apply the yaml file to create pod.

**Command:**
```bash
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
```

**Command:**
```bash
kubectl apply -f pod-nginx.yaml
```

**Verification Command:**  
![](./screenshot/06.png)

---

### 7. Create ReplicaSet with 3 replicas using nginx Image.

**Explanation:**
  - A ReplicaSet ensures a specific number of Pod replicas are always running. If a Pod fails or is deleted, the ReplicaSet creates a new one to maintain the count.


**Command:**
```bash
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
      - name: nginx-container
        image: nginx
```

**Command:**
```bash
kubectl apply -f ReplicaSet.yaml
kubectl get replicasets
kubectl get pods
```

**Verification Command:**  
![](./screenshot/07.png)

---

### 8. Scale the replicas to 5 without edit in the Yaml file.

**Explanation:**
  - we can scale up or down the nunber of replica by using `kubectl scale` .

**Command:**
```bash
kubectl scale replicaset --replicas=5 frontend
kubectl describe replicaset frontend | grep -i replica  # grep for number of replica
```

**Verification Command:**  
![](./screenshot/08.png)

---

