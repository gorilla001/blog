### Deployment 

+ CREATE 

```
POST /apis/apps/v1/namespaces/{namespace}/deployments
```

```
cat deployment.yml
```

```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: deployment-example
spec:
  replicas: 3
  revisionHistoryLimit: 10
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx  
      image: nginx:1.10
      ports:
      - containerPort: 80
```
```
kubectl create -f deployment.yml
```
+ PATCH

```
PATCH /apis/apps/v1/namespaces/{namespace}/deployments/{name}
```

+ REPLACE

```
PUT /apis/apps/v1/namespaces/{namespace}/deployments/{name}
```

```
body
```
```
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: deployment-example
spec:
  replicas: 3
  revisionHistoryLimit: 10
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.11
        ports:
        - containerPort: 80
```
```
kubectl replace -f replace.yml
```

+ DELETE

```
DELETE /apis/apps/v1/namespaces/{namespace}/deployments/{name}
```

```
kubectl delete deployment deployment-example
```

```
DELETE /apis/apps/v1/namespaces/{namespace}/deployments
```

+ GET

```
GET /apis/apps/v1/namespaces/{namespace}/deployments/{name}
```
```
kubectl get deployment deployment-example -o json
```
```
{
  "kind": "Deployment",
  "apiVersion": "apps/v1beta1",
  "metadata": {
    "name": "deployment-example",
    "namespace": "default",
    "selfLink": "/apis/apps/v1beta1/namespaces/default/deployments/deployment-example",
    "uid": "1b33145a-9c63-11e6-9c54-42010a800148",
    "resourceVersion": "2064726",
    "generation": 4,
    "creationTimestamp": "2016-10-27T16:33:35Z",
    "labels": {
      "app": "nginx"
    },
    "annotations": {
      "deployment.kubernetes.io/revision": "1"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "creationTimestamp": null,
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.10",
            "ports": [
              {
                "containerPort": 80,
                "protocol": "TCP"
              }
            ],
            "resources": {},
            "terminationMessagePath": "/dev/termination-log",
            "imagePullPolicy": "IfNotPresent"
          }
        ],
        "restartPolicy": "Always",
        "terminationGracePeriodSeconds": 30,
        "dnsPolicy": "ClusterFirst",
        "securityContext": {}
      }
    },
    "strategy": {
      "type": "RollingUpdate",
      "rollingUpdate": {
        "maxUnavailable": 1,
        "maxSurge": 1
      }
    }
  },
  "status": {
    "observedGeneration": 4,
    "replicas": 3,
    "updatedReplicas": 3,
    "availableReplicas": 3
  }
}
```

+ LIST

```
GET /apis/apps/v1/namespaces/{namespace}/deployments
```
```
kubectl get deployment -o json
```
```
{
  "kind": "List",
  "apiVersion": "v1",
  "metadata": {},
  "items": [
    {
      "kind": "Deployment",
      "apiVersion": "app/v1beta1",
      "metadata": {
        "name": "docs",
        "namespace": "default",
        "selfLink": "/apis/app/v1beta1/namespaces/default/deployments/docs",
        "uid": "ef49e1d2-915e-11e6-be81-42010a80003f",
        "resourceVersion": "1924126",
        "generation": 21,
        "creationTimestamp": "2016-10-13T16:06:00Z",
        "labels": {
          "run": "docs"
        },
        "annotations": {
          "deployment.kubernetes.io/revision": "10",
          "replicatingperfection.net/push-image": "true"
        }
      },
      "spec": {
        "replicas": 1,
        "selector": {
          "matchLabels": {
            "run": "docs"
          }
        },
        "template": {
          "metadata": {
            "creationTimestamp": null,
            "labels": {
              "auto-pushed-image-pwittrock/api-docs": "1477496453",
              "run": "docs"
            }
          },
          "spec": {
            "containers": [
              {
                "name": "docs",
                "image": "pwittrock/api-docs:v9",
                "resources": {},
                "terminationMessagePath": "/dev/termination-log",
                "imagePullPolicy": "Always"
              }
            ],
            "restartPolicy": "Always",
            "terminationGracePeriodSeconds": 30,
            "dnsPolicy": "ClusterFirst",
            "securityContext": {}
          }
        },
        "strategy": {
          "type": "RollingUpdate",
          "rollingUpdate": {
            "maxUnavailable": 1,
            "maxSurge": 1
          }
        }
      },
      "status": {
        "observedGeneration": 21,
        "replicas": 1,
        "updatedReplicas": 1,
        "availableReplicas": 1
      }
    },
    {
      "kind": "Deployment",
      "apiVersion": "app/v1beta1",
      "metadata": {
        "name": "deployment-example",
        "namespace": "default",
        "selfLink": "/apis/app/v1beta1/namespaces/default/deployments/deployment-example",
        "uid": "1b33145a-9c63-11e6-9c54-42010a800148",
        "resourceVersion": "2064726",
        "generation": 4,
        "creationTimestamp": "2016-10-27T16:33:35Z",
        "labels": {
          "app": "nginx"
        },
        "annotations": {
          "deployment.kubernetes.io/revision": "1"
        }
      },
      "spec": {
        "replicas": 3,
        "selector": {
          "matchLabels": {
            "app": "nginx"
          }
        },
        "template": {
          "metadata": {
            "creationTimestamp": null,
            "labels": {
              "app": "nginx"
            }
          },
          "spec": {
            "containers": [
              {
                "name": "nginx",
                "image": "nginx:1.10",
                "ports": [
                  {
                    "containerPort": 80,
                    "protocol": "TCP"
                  }
                ],
                "resources": {},
                "terminationMessagePath": "/dev/termination-log",
                "imagePullPolicy": "IfNotPresent"
              }
            ],
            "restartPolicy": "Always",
            "terminationGracePeriodSeconds": 30,
            "dnsPolicy": "ClusterFirst",
            "securityContext": {}
          }
        },
        "strategy": {
          "type": "RollingUpdate",
          "rollingUpdate": {
            "maxUnavailable": 1,
            "maxSurge": 1
          }
        }
      },
      "status": {
        "observedGeneration": 4,
        "replicas": 3,
        "updatedReplicas": 3,
        "availableReplicas": 3
      }
    }
  ]
}
```

### ReplicaSet

+ CREATE

```
POST /apis/apps/v1beta2/namespaces/{namespace}/replicasets
```

```
apiVersion: extensions/v1beta1
kind: ReplicaSet
metadata:
  # Unique key of the ReplicaSet instance
  name: replicaset-example
spec:
  # 3 Pods should exist at all times.
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      # Run the nginx image
      - name: nginx
        image: nginx:1.10
```

```
kubectl create -f replicaset.yml
```

+ PATCH

```
PATCH /apis/apps/v1beta2/namespaces/{namespace}/replicasets/{name}
```

+ REPLIACE

```
PUT /apis/apps/v1beta2/namespaces/{namespace}/replicasets/{name}
```

+ DELETE

```
DELETE /apis/apps/v1beta2/namespaces/{namespace}/replicasets/{name}
```

```
DELETE /apis/apps/v1beta2/namespaces/{namespace}/replicasets
```


