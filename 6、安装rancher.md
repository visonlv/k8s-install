sudo docker run -d --restart=unless-stopped --privileged --name rancher -p 20080:80 -p 443:443 rancher/rancher

    kubectl apply -f https://192.168.31.244/v3/import/855fd5n6s8gjl6cfnsndnfjlmcvlhqxsdv7sztrbj5l2kghld8q966_c-m-s6nf2k8r.yaml

    curl --insecure -sfL https://192.168.31.244/v3/import/855fd5n6s8gjl6cfnsndnfjlmcvlhqxsdv7sztrbj5l2kghld8q966_c-m-s6nf2k8r.yaml | kubectl apply -f -

    kubectl create clusterrolebinding cluster-admin-binding --clusterrole cluster-admin --user <your username from your kubeconfig>

sudo docker system prune
sudo systemctl restart kubelet


--force --grace-period=0

 "finalizers": [
        ],
        
kubectl get ns cattle-system -o json > cattle-system.json
kubectl proxy --port=8081
curl -k -H "Content-Type: application/json" -X PUT --data-binary @cattle-system.json http://127.0.0.1:8081/api/v1/namespaces/cattle-system/finalize
```