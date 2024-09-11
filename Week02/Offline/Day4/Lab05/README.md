- What is a Service in Kubernetes, and why is it needed?

- What are the different types of Services in Kubernetes (e.g., ClusterIP, NodePort) and what are their use cases?

- what ar LoadBalancer, ExternalName service in kuberenetes and what are their use cases?

- How does a Kubernetes Service use selectors to identify the Pods it routes traffic to? Can a Service be created without a selector?

- Explain how a NodePort service works in Kubernetes. What are its advantages and limitations?

- What is a Headless Service in Kubernetes, and when would you use it? How does it differ from a standard ClusterIP service?

- Create a ClusterIP Service:
	Write a YAML definition for a ClusterIP service that exposes a deployment named my-app running on port 8080. Ensure the service maps to port 80 inside the cluster.

- Set up a NodePort Service:
	Create a NodePort service that exposes a deployment named backend on port 30001 of each node. Verify that the service is accessible externally via the node’s IP and port 30001.

- Test Service with Selectors:
	Create a ClusterIP service named web-service with the selector app: 0ld-web. Deploy two sets of Pods, one with the label app: old-web and another with the label app: api. Verify that only the web Pods receive traffic.

- Change Service Selector:
	Update an existing service to change its selector from app: old-web to app: new-web. Verify that the traffic is now routed only to Pods with the new label.

- Configure a Service for Multiple Ports:
	Define a service that exposes multiple ports (e.g., 80 for HTTP and 443 for HTTPS) on a deployment named multi-port-app "get the front in app from your own choice". Verify both ports are accessible within the cluster.
