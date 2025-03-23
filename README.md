# rhoai-tests

Use this repository to test RHOAI deployments on NERC OpenShift clusters. 

The tests are designed to ensure the proper installation and functioning of RHOAI deployements following fresh installs, cluster/operator upgrades, and hardware changes.

## Prerequisites

Access to an RHOAI Project with permissions to access and deploy workloads to GPUs.

For these RHOAI tests, you will need two S3-compatible object storage buckets, such as NERC OpenStack Container (Ceph), MinIO, or AWS S3. You can either use your own storage buckets or apply the the kustomization file under: [make link here]() to configure minio a deployment for tests. 

Using the provided minio deployment will create the following:

- 2 minio object buckets:
	- my-storage – Use this bucket to store your models and data.

	- pipeline-artifacts – Use this bucket to store pipeline artifacts. A pipeline artifacts bucket is required when setting up a pipeline server.

- Establishes two connections in your project - one for each bucket - using the same generated credentials.

- Deployment of MinIO instance in your project namespace.

- Generates a random user ID and password for the MinIO instance.

- Installs all required network rbac policies.

> **MinIO Web Console Login Credentials** The deployed Minio console creds can be found in the data connections created in your RHOAI project's data connections menu.

> Or run: `oc get secret minio-root-user -o template --template '{{.data.MINIO_ROOT_USER}}' | base64 --decode` && `oc get secret minio-root-user -o template --template '{{.data.MINIO_ROOT_PASSWORD}}' | base64 --decode`

## Create a Pipeline Server

In the Configure pipeline server form, in the Access key field next to the key icon, click the dropdown menu and then click Pipeline Artifacts to populate the Configure pipeline server form with credentials for the connection.

![Import Pipeline Artifacts](ds-project-create-pipeline-server-form.png)

Leave the database configuration as the default and click Configure pipeline server.

## Create a Workbench and Notebook Server


