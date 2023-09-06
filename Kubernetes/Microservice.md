## Commands
| Commands| Function  |
|----------|----------|
| `docker run -d --name=redis redis`  |  run container named redis with image reids in background (-d) |
| `docker run -d --name=vote -p 5000:80 --link redis:redis voting-app`  | link redis to the vote container app; link is deprecated   |
| `kubectl get pod,svc`  | view pods and services   |