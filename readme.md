#port-forward-to-get-web-interface
kubectl port-forward svc/airflow 8080:8080 -n airflow


#Ensure the database is initialized by running the following
kubectl exec -it <airflow-pod-name> -n airflow -- airflow db init


#Airflow User Creation: Create an admin user for Airflow:
kubectl exec -it <airflow-pod-name> -n airflow -- airflow users create --username admin --password admin --firstname Admin --lastname User --role Admin --email admin@example.com

