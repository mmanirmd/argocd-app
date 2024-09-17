# argocd-app

When backing up an on-prem GKE (Google Kubernetes Engine) cluster using Commvault, it's important to ensure that all critical resources are backed up to allow a smooth restore in case of failure. Here’s a list of resources you should consider for backup, along with test cases for each resource:

### 1. **Kubernetes Cluster Configuration**
   - **Resources to Backup**:
     - Cluster configuration files
     - RBAC policies
     - Node configurations
   - **Test Cases**:
     - **Backup Test**: Verify that the configuration files for the cluster are correctly backed up and stored.
     - **Restore Test**: Restore the cluster using the configuration files and verify that the cluster is in the exact state before backup, including network settings and node pools.
     - **Validation Test**: Ensure that RBAC policies are applied correctly post-restore and that all nodes are functional and ready.

### 2. **Namespaces**
   - **Resources to Backup**:
     - All namespaces used within the cluster.
   - **Test Cases**:
     - **Backup Test**: Validate that the namespaces, including their configurations, are backed up.
     - **Restore Test**: Restore namespaces individually and validate that the resources within the namespace are intact.
     - **Validation Test**: Ensure that after the restore, namespace resource quotas, limits, and policies are maintained.

### 3. **Pods and Deployments**
   - **Resources to Backup**:
     - Pods and deployment specifications.
   - **Test Cases**:
     - **Backup Test**: Check that all active deployments, including their replicas, volumes, and configurations, are backed up.
     - **Restore Test**: Restore the deployment and verify that the pods are running as expected and that all volume mounts and configurations are correct.
     - **Validation Test**: Ensure that the application deployed in the restored pods functions correctly and that scaling policies work.

### 4. **Persistent Volumes (PVs) and Persistent Volume Claims (PVCs)**
   - **Resources to Backup**:
     - PVs and their associated PVCs, which hold the data for stateful applications.
   - **Test Cases**:
     - **Backup Test**: Ensure that the data from PVs is successfully backed up.
     - **Restore Test**: Restore the PVC and verify that the PVs get bound correctly, and data consistency is maintained after restoration.
     - **Validation Test**: Validate that applications using these volumes (e.g., databases) are able to read/write data without errors.

### 5. **ConfigMaps and Secrets**
   - **Resources to Backup**:
     - ConfigMaps (used for configuration) and Secrets (used for sensitive data).
   - **Test Cases**:
     - **Backup Test**: Verify that all ConfigMaps and Secrets are backed up securely (ensuring Secrets are encrypted).
     - **Restore Test**: Restore the ConfigMaps and Secrets and ensure that the applications retrieve them correctly.
     - **Validation Test**: Ensure that after restore, applications dependent on these ConfigMaps and Secrets function properly, without configuration or authentication issues.

### 6. **Services (ClusterIP, NodePort, LoadBalancer)**
   - **Resources to Backup**:
     - All types of Kubernetes services, including their IPs and configurations.
   - **Test Cases**:
     - **Backup Test**: Verify that the service configurations are correctly backed up.
     - **Restore Test**: Restore the services and ensure the IP addresses, ports, and load balancer settings are retained.
     - **Validation Test**: Ensure that services are accessible as expected after the restore, and that traffic routing works as before.

### 7. **Ingress Resources**
   - **Resources to Backup**:
     - Ingress rules and configurations.
   - **Test Cases**:
     - **Backup Test**: Validate that ingress rules and certificates are backed up.
     - **Restore Test**: Restore the ingress resources and verify that they route traffic to the correct services.
     - **Validation Test**: Confirm that HTTPS and HTTP traffic are handled correctly post-restore, including checking SSL certificates.

### 8. **StatefulSets**
   - **Resources to Backup**:
     - Stateful applications like databases or other apps requiring persistent identity.
   - **Test Cases**:
     - **Backup Test**: Verify that StatefulSets and their associated volumes are backed up.
     - **Restore Test**: Restore StatefulSets and ensure that each replica gets the correct persistent identity.
     - **Validation Test**: Ensure that the applications dependent on StatefulSets work properly after restore, including volume persistence.

### 9. **DaemonSets**
   - **Resources to Backup**:
     - DaemonSets configurations.
   - **Test Cases**:
     - **Backup Test**: Ensure that DaemonSet configurations and deployments are backed up.
     - **Restore Test**: Restore DaemonSets and verify that they are scheduled properly on all relevant nodes.
     - **Validation Test**: Ensure that post-restore, DaemonSets run on the correct nodes and their intended functions are maintained.

### 10. **CronJobs and Jobs**
   - **Resources to Backup**:
     - Scheduled jobs (CronJobs) and one-time jobs.
   - **Test Cases**:
     - **Backup Test**: Verify that all job configurations are backed up.
     - **Restore Test**: Restore CronJobs and Jobs, and validate that they are scheduled/running as expected.
     - **Validation Test**: Ensure that CronJobs are triggering at their defined intervals post-restore, and one-time jobs are executed successfully.

### 11. **Service Accounts, Roles, and RoleBindings**
   - **Resources to Backup**:
     - Service accounts, RBAC roles, and their bindings.
   - **Test Cases**:
     - **Backup Test**: Validate that the service accounts and their permissions are backed up.
     - **Restore Test**: Restore the service accounts and ensure that they are functional with the correct role bindings.
     - **Validation Test**: Ensure that applications and users have the expected access to the cluster resources post-restore.

### 12. **Network Policies**
   - **Resources to Backup**:
     - Network policies that define how pods communicate with each other and with services.
   - **Test Cases**:
     - **Backup Test**: Verify that all network policies are backed up.
     - **Restore Test**: Restore network policies and verify that they are applied correctly.
     - **Validation Test**: Confirm that the restored policies work as expected, preventing or allowing communication as per the original configuration.

### Summary of Test Cases
- **Backup Test**: Check that all resource data is correctly captured.
- **Restore Test**: Validate the restoration of resources.
- **Validation Test**: Ensure that applications, configurations, and dependencies are functional post-restore and that performance or behaviors remain consistent.

Ensure that your backups are automated and periodic, and schedule regular tests of restoration procedures to identify any issues before actual disasters happen.
