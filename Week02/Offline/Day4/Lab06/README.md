1- What is a volume in Kubernetes, and how does it differ from a container's storage?

2- What are the different types of volumes available in Kubernetes? Describe at least three types and their use cases.

3- How do PersistentVolumes (PVs) and PersistentVolumeClaims (PVCs) work together in Kubernetes? Explain their relationship and purpose.

4- Create a Pod with an emptyDir volume:
	Write a YAML definition for a Pod that uses an emptyDir volume to share data between two containers within the Pod. Deploy the Pod and verify that the data is shared.

5- Set up a Pod with a hostPath volume:
	Define a Pod that mounts a hostPath volume to access files from the host node’s file system. Deploy the Pod and verify that it can read/write to the specified directory on the host.

6- Deploy a PersistentVolume (PV) and PersistentVolumeClaim (PVC):
	Create a YAML file to define a PersistentVolume of 5Gi with ReadWriteOnce access mode. Then, create a PersistentVolumeClaim requesting 2Gi of storage from this PV. Deploy both resources and verify the PVC is bound to the PV.

7- Create a Pod that uses a PVC:
	Write a YAML definition for a Pod that uses the PVC created in Exercise 3. Mount the PVC to a specific path inside the container and test that the storage is accessible.

8- Dynamic Provisioning of Persistent Volumes:
	Create a StorageClass that uses a dynamic provisioner (e.g., AWS EBS, GCE Persistent Disk, or NFS). Deploy a PVC that requests storage dynamically using this StorageClass. Verify that the storage is dynamically provisioned.

9- Use a configMap as a Volume:
	Create a ConfigMap with some configuration data. Write a Pod YAML definition that mounts this ConfigMap as a volume and verify the data is correctly mounted and accessible inside the container.

10- Create a Pod with a secret as a Volume:
	Define a Kubernetes Secret containing sensitive data. Create a Pod that mounts this secret as a volume and verify the data is correctly mounted and accessible inside the container in a secure way.

11- Set up a Pod with a gitRepo volume:
	Write a YAML definition for a Pod that uses a gitRepo volume to clone a Git repository into the container. Verify that the repository's contents are available inside the container.

12- Resize a Persistent Volume Claim (PVC):
	Create a PVC and bind it to a Pod. After deployment, resize the PVC to request more storage (assuming the underlying storage provider supports resizing). Verify that the PVC has been resized successfully.

13- Use subPath for mounting volumes:
	Create a Pod with a single volume and use the subPath feature to mount different subdirectories of that volume to different paths within a container. Verify that each path in the container corresponds to the correct subdirectory on the volume.
