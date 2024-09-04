
# Airflow with Kubernetes and Persistent Volume (PV)

This repository contains the Kubernetes configurations to deploy Apache Airflow with Persistent Volume (PV) support. It helps set up Airflow with a fully functional web interface, along with PostgreSQL as the backend, utilizing Kubernetes for scheduling Airflow workloads.

## Features

- Deploy Apache Airflow using Kubernetes.
- Persistent Volume support for data persistence.
- PostgreSQL database as the Airflow backend.
- Easy access to the Airflow web interface using `kubectl port-forward`.
- Simple commands to initialize the database and create users.

## Prerequisites

- A Kubernetes cluster
- `kubectl` installed and configured
- `helm` installed (optional but recommended for managing deployments)
- Persistent Volume (PV) available in the cluster

## Usage

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/airflow-with-k8s-and-pv.git
cd airflow-with-k8s-and-pv
```

### 2. Create the Namespace

```bash
kubectl apply -f namespace.yaml
```

### 3. Set up PostgreSQL

```bash
kubectl apply -f postgres.yaml
```

### 4. Set up Persistent Volume

```bash
kubectl apply -f pv.yaml
```

### 5. Deploy Apache Airflow

```bash
kubectl apply -f airflow-config.yaml
kubectl apply -f airflow-deployment.yaml
kubectl apply -f airflow-pods-operator-scheduler.yaml
```

### 6. Access the Airflow Web Interface

To access the Airflow web interface, use `kubectl port-forward` to forward the service to your local machine:

```bash
kubectl port-forward svc/airflow 8080:8080 -n airflow
```

Now you can access the Airflow web interface at `http://localhost:8080`.

### 7. Initialize the Database

Ensure the database is initialized by running the following command:

```bash
kubectl exec -it <scheduler-pod-name> -n airflow -- airflow db init
```

Replace `<scheduler-pod-name>` with the name of your Airflow scheduler pod.

### 8. Create an Admin User

You can create an admin user for Airflow using the following command:

```bash
kubectl exec -it <scheduler-pod-name> -n airflow -- airflow users create \
    --username admin --password admin \
    --firstname Admin --lastname User \
    --role Admin --email admin@example.com
```

### 9. Monitor the Airflow Pods

To check the status of the Airflow pods, use:

```bash
kubectl get pods -n airflow
```

## File Descriptions

- `airflow-config.yaml`: Configuration for the Airflow deployment.
- `airflow-deployment.yaml`: YAML file for the main Airflow deployment.
- `airflow-pods-operator-scheduler.yaml`: Configures the Airflow pods, operator, and scheduler.
- `namespace.yaml`: Namespace configuration for isolating Airflow in its own namespace.
- `postgres.yaml`: PostgreSQL configuration file for the database backend.
- `pv.yaml`: Persistent Volume setup for Airflow.

## Requirements

- Kubernetes Cluster (Minikube, GKE, etc.)
- Helm (optional)
- `kubectl` installed and configured

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contributions

Contributions are welcome! Feel free to open an issue or submit a pull request.

## Author

[Imrul](https://github.com/yourusername)

## Contact

For any inquiries, please contact me at [hello@imrul.net](mailto:hello@imrul.net).
