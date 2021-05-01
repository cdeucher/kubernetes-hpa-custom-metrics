Setup:

Build the image: 

1. docker build -t nginx-vts:1.0 .  
2. docker build -t prometheus:latest . 
3. kube create -f namespaces.yml
4. kube create -f kubernetes-metrics-server/
5. kube create -f prometheus-deployment/
6. kube create -f prometheus-adapter/
7. kube create -f nginx-deployment.yml
8. kube create -f nginx-hpa.yml

Test:

1. kubectl port-forward service/prometheus 9090:9090 -n monitoring
2. http://localhost:9090/targets
3. kubectl port-forward deployment.apps/nginx-deployment 8080:80 -n nginx
4. http://localhost:8080/status/format/prometheus
5. while true; do curl -d "quantity=1" -X GET http://localhost:8080/status/format/json ;  done

Commands:

- kubectl get --raw "/apis/" | jq .
- kubectl get --raw "/apis/metrics.k8s.io/v1beta1/nodes" | jq .
- kubectl get --raw "/apis/metrics.k8s.io/v1beta1/pods" | jq .
- kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta1" | jq .
- kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta1/namespaces/nginx/pods/*/nginx_vts_server_request_seconds" | jq .

