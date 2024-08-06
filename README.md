# Airflow on EKS

This repository contains instructions and manifests for deploying Apache Airflow on an existing EKS cluster using Helm. I am using the Kubernetes Executor for scalability and flexibility, and logs from workers will appear in Airflow's console. New DAGs are deployed using a Git-Sync sidecar container.

## Prerequisites

- Kubernetes cluster (EKS)
- Helm installed
- Access to the cluster with `kubectl`

## Installation

```sh
helm repo add apache-airflow https://airflow.apache.org
helm repo update
helm install airflow apache-airflow/airflow -n airflow --create-namespace -f values.yaml
```

## DAG Deployment

I am using a Git-Sync sidecar container to manage DAG deployments. This method ensures that the DAGs are always up-to-date with the repository and we can utilize GitOps approach. 

The Git-Sync sidecar container syncs the DAGs from a specified Git repository to the Airflow scheduler and worker pods. The sync process runs at regular intervals to ensure the DAGs are updated.

Using a Git-Sync sidecar container is a straightforward and efficient way to manage DAGs in a Kubernetes environment. It allows for easy version control and collaboration on DAGs, ensuring that the Airflow instance always runs the latest DAG definitions.
