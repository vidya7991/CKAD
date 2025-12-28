Task 1: Application Creation and Resource Allocation
Create a Deployment named my-app-deploy using the image nginx:latest.
The Deployment must run exactly 3 replicas.
The Pods must specify a CPU Request of $100\text{m}$ and a Memory Request of $128\text{Mi}$.
The Pods must specify a CPU Limit of $200\text{m}$ and a Memory Limit of $256\text{Mi}$.
Tip: Use the -o yaml --dry-run=client flags to generate the YAML manifest first, then use kubectl apply -f to create the resource.


