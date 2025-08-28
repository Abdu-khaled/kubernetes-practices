# kubernetes-practices

## Part1:

### 1. create pod nginx with name my nginx direct from command don't use yaml file.

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

### 2. create pod nginx with name my nginx command and use Image nginx123  direct from command don't use yaml file.

**Explanation:**
 - To create pod nginx without yaml file we use imperative way by use `kubectl run`. 
**Command:**
```bash
 kubectl run my-nginx --image nginx123
 kubectl get pods
```

**Verification Command:**  
![](./screenshot/02.png)
