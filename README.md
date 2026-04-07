# GitOps J4F

` kubectl create secret docker-registry regcred --docker-username=YOUR_USERNAME --docker-password=YOUR_PASSWORD --docker-email=YOUR_EMAIL -n pizza `

`nohup kubectl port-forward svc/argocd-server -n argocd 8080:443 >/dev/null 2>&1 &`

`kubectl port-forward svc/pizza-be -n pizza 3000:3000 >/dev/null 2>&1 &`

`kubectl port-forward svc/pizza-fe -n pizza 8081:80 >/dev/null 2>&1 &`

`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d`