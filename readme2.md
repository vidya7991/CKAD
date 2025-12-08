1. Pod and Multi-Container (12 Minutes)
A new application requires two containers running in a single Pod.

Create a Namespace named ckad-q1.

Create a Pod named multi-log-pod in the ckad-q1 namespace.

The Pod should have two containers:

Container A: Name: logger-a, Image: busybox, Command: ["/bin/sh", "-c", "while true; do echo 'Log A: $(date)' >> /var/log/app.log; sleep 5; done"].

Container B: Name: logger-b, Image: busybox, Command: ["/bin/sh", "-c", "while true; do echo 'Log B: $(date)' >> /var/log/app.log; sleep 5; done"].

Both containers must share a single volume named log-volume mounted at /var/log within each container.

Troubleshoot: After creation, ensure the Pod is running and has both containers logging to the same file. Use kubectl logs and kubectl exec to verify the combined output.

2. ConfigMaps and Environment Variables (12 Minutes)
A web application needs configuration data passed via environment variables.

Ensure you are working in the default namespace.

Create a ConfigMap named app-settings with the following key/value pairs:

UI_COLOR: blue

API_URL: http://api.backend.svc.cluster.local

Create a Deployment named web-app-deploy with 3 replicas using the image nginx.

Configure the Deployment's Pods to expose the data from the app-settings ConfigMap as environment variables inside the containers, using the original ConfigMap keys as the variable names.

Verification: Confirm that a Pod created by the Deployment has the UI_COLOR environment variable set to blue.

3. Services and Exposure (12 Minutes)
You need to expose an existing application running on an internal port.

Context: A Deployment named backend-api exists in the default namespace. The application inside its Pods listens on port 8080.

Create a Service named api-service that targets the backend-api Pods (assume they have the label app=backend-api).

The Service should be of type NodePort and expose the application on port 80 internally, mapping to the target port 8080.

The NodePort value must be set to 30080.

Verification: Use kubectl describe svc api-service to confirm the ports are correctly configured, and demonstrate connectivity using a simple curl command (simulating a test from an outside node). Note: The cluster environment for the exam will provide an IP/Node to test against.

4. Persistent Volume Claim (12 Minutes)
A database application needs persistent storage.

Create a PersistentVolumeClaim (PVC) named db-data-pvc with:

Access Mode: ReadWriteOnce

Storage Request: 1Gi

Storage Class: (Assume a default storage class is available, or omit if none is specified by the problem).

Create a Pod named db-pod using the image mongo:4.0.

Mount the db-data-pvc volume to the container at the path /data/db.

Verification: Check the status of the PVC and the Pod to ensure the volume is successfully bound and mounted.

5. Troubleshooting and Rollback (12 Minutes)
A Deployment update has failed and needs to be reverted.

Context: A Deployment named frontend in the default namespace is currently running and stable with the image nginx:latest.

Scenario: An attempt was made to update the Deployment with a non-existent image (nginx:non-existent-tag).

Simulate this by running: kubectl set image deployment/frontend nginx=nginx:non-existent-tag --record

Troubleshoot: Identify the problem causing the rollout to fail or get stuck. Check the Deployment status, ReplicaSet events, and Pod logs/events.

Action: Perform a rollback to the previous, successful version of the Deployment.

Verification: Verify that the Deployment's Pods are running the correct nginx:latest image again.