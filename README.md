# GitOps J4F

 kubectl create secret docker-registry regcred --docker-username=YOUR_USERNAME --docker-password=YOUR_PASSWORD --docker-email=YOUR_EMAIL -n pizza 

kubectl create secret generic pizza-be-secret   --from-env-file=.env.be   --namespace=pizza   --dry-run=client -o yaml > pizza-be-secrets.yaml

kubeseal   --format yaml   --controller-name sealed-secrets   --controller-namespace kube-system   --namespace pizza   < pizza-be-secrets.yaml > pizza-be-sealed-secrets.yaml

kubectl apply -f pizza-be-sealed-secrets.yaml

kubectl rollout restart deployment -n argocd

kubectl port-forward svc/argocd-server -n argocd 8080:443 >/dev/null 2>&1 &

kubectl port-forward svc/pizza-be -n pizza 3000:3000 >/dev/null 2>&1 &

kubectl port-forward svc/pizza-fe -n pizza 8082:80 >/dev/null 2>&1 &

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d