# Kubernetes Basic Commands

Kubernetes is a container orchestration platform used to automate deployment, scaling, and lifecycle management of containerized applications.
Below is a curated list of essential `kubectl` commands useful for daily DevOps and platform engineering tasks.

---

## 1. Cluster & Context Management

| Command                                     | Description                                  |
| ------------------------------------------- | -------------------------------------------- |
| `kubectl version --short`                   | Display client and server versions           |
| `kubectl cluster-info`                      | Show Kubernetes master and service endpoints |
| `kubectl config view`                       | View kubeconfig configuration                |
| `kubectl config get-contexts`               | List all available contexts                  |
| `kubectl config use-context <context-name>` | Switch context between clusters              |
| `kubectl get nodes`                         | List worker and control plane nodes          |

---

## 2. Pods

| Command                                       | Description                             |
| --------------------------------------------- | --------------------------------------- |
| `kubectl get pods`                            | List pods in the current namespace      |
| `kubectl get pods -A`                         | List pods across all namespaces         |
| `kubectl describe pod <pod-name>`             | Show detailed information about a pod   |
| `kubectl logs <pod-name>`                     | Retrieve logs from a pod                |
| `kubectl logs <pod-name> -c <container-name>` | Retrieve logs from a specific container |
| `kubectl exec -it <pod-name> -- /bin/bash`    | Open interactive shell inside a pod     |
| `kubectl delete pod <pod-name>`               | Delete a pod                            |

---

## 3. Deployments

| Command                                                   | Description                              |
| --------------------------------------------------------- | ---------------------------------------- |
| `kubectl create deployment <name> --image=<image>`        | Create a deployment                      |
| `kubectl get deployments`                                 | List deployments                         |
| `kubectl describe deployment <name>`                      | Show deployment details                  |
| `kubectl scale deployment <name> --replicas=<num>`        | Scale a deployment                       |
| `kubectl set image deployment/<name> <container>=<image>` | Update container image within deployment |
| `kubectl rollout status deployment/<name>`                | Check deployment rollout status          |
| `kubectl rollout undo deployment/<name>`                  | Roll back to previous deployment version |
| `kubectl delete deployment <name>`                        | Delete a deployment                      |

---

## 4. Services

| Command                                                          | Description                    |
| ---------------------------------------------------------------- | ------------------------------ |
| `kubectl get svc`                                                | List services                  |
| `kubectl expose deployment <name> --type=NodePort --port=<port>` | Expose deployment as a service |
| `kubectl describe svc <name>`                                    | Show service details           |
| `kubectl delete svc <name>`                                      | Delete a service               |

---

## 5. Namespaces

| Command                           | Description        |
| --------------------------------- | ------------------ |
| `kubectl get ns`                  | List namespaces    |
| `kubectl create namespace <name>` | Create a namespace |
| `kubectl delete namespace <name>` | Delete a namespace |

---

## 6. ConfigMaps & Secrets

| Command                                                             | Description            |
| ------------------------------------------------------------------- | ---------------------- |
| `kubectl create configmap <name> --from-literal=<key>=<value>`      | Create a ConfigMap     |
| `kubectl get configmaps`                                            | List ConfigMaps        |
| `kubectl describe configmap <name>`                                 | Show ConfigMap details |
| `kubectl create secret generic <name> --from-literal=<key>=<value>` | Create a Secret        |
| `kubectl get secrets`                                               | List Secrets           |
| `kubectl describe secret <name>`                                    | Show Secret details    |

---

## 7. Cleanup Operations

| Command                         | Description                             |
| ------------------------------- | --------------------------------------- |
| `kubectl delete all --all`      | Delete all resources in a namespace     |
| `kubectl delete -f <file>.yaml` | Delete resources defined in a YAML file |

---

## 8. Working with YAML Manifests

Applying and deleting resources from configuration files:

```bash
kubectl apply -f <file>.yaml
kubectl delete -f <file>.yaml
```

---
