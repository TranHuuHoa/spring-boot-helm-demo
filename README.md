cd demoweb
chmod +x mvnw
docker-compose build
docker-compose up
Visit http://localhost:8080/

docker build -t tranhuuhoa/spring-boot-helm-demo .
docker push tranhuuhoa/spring-boot-helm-demo
# deploy using helm
cd demoweb/charts
helm install demo ./springboot-demoweb/ 

# Access demo application following NOTES:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=springboot-demoweb,app.kubernetes.io/instance=demo" -o jsonpath="{.items[0].metadata.name}")
  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT

# Uninstall demo application in cluster:
helm uninstall demo


