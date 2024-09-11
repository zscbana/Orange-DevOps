- What is RBAC in Kubernetes, and why is it important?
- What are the main components of RBAC in Kubernetes? Describe the purpose of each.
- How do Roles differ from ClusterRoles in Kubernetes?
- What is a RoleBinding in Kubernetes, and how does it differ from a ClusterRoleBinding?
- How can you list all the Roles and RoleBindings in a specific namespace?

- How do you create a Role that allows a user to read secrets only in a specific namespace? Provide a YAML example.
- Explain how ClusterRoleBindings can be used to grant permissions across the entire Kubernetes cluster.
- What are Subjects in RBAC, and what types of subjects can be used in RoleBindings or ClusterRoleBindings?
- How can you check the permissions of a particular user or service account in a Kubernetes cluster?
- What is the significance of the aggregate-to-admin, aggregate-to-edit, and aggregate-to-view labels in Kubernetes RBAC?

- How does Kubernetes RBAC integrate with external identity providers (e.g., LDAP, OIDC)?
- How do you troubleshoot RBAC permission errors in Kubernetes? What are some common issues?
- Explain how to grant temporary elevated privileges to a user in Kubernetes. What are the security implications?
- What is the difference between using RBAC and Kubernetes' native ServiceAccount permissions for pods?
- How can you restrict access to certain Kubernetes API groups or resources using RBAC? Provide a YAML example.

- Write a YAML definition for a ClusterRole that allows listing all pods in any namespace.
- Create a Role that allows a user to create, update, and delete deployments only within the dev namespace.
- Set up a RoleBinding that assigns the view role to a user named john in the testing namespace. Provide the YAML.
- Deploy a ClusterRoleBinding that grants the edit role to a service account named developer in all namespaces.
- Write a command to check if a user named alice has permission to delete pods in the production namespace.

- Write a YAML definition for a Role named pod-executor in the ci-cd namespace that allows creating, listing, and executing Pods. Bind this role to a service account named pipeline-sa using a RoleBinding.
- Create a Role named "persistent-volume-access" in the storage namespace that grants permissions to create and delete PersistentVolumeClaims. Assign this role to a service account named storage-admin using a RoleBinding.
- Create a ClusterRole named readonly-cluster that grants read-only access to all resources across the cluster. Then, create a ClusterRoleBinding that assigns this role to a user named alice.