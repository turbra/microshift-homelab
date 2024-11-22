# Install and configure ArgoCD

1. Install the ArgoCD CRD and create a `ClusterRoleBinding` and `Route`.

   ```bash
   oc apply -f setup/
   while ! oc wait crd applications.argoproj.io --timeout=-1s --for=condition=Established  2>/dev/null; do sleep 30; done
   ```

2. Retrieve admin login details

   ```bash
   echo $(oc get route -n argocd argocd-server -o template --template='https://{{.spec.host}}')

   oc extract secrets/argocd-initial-admin-secret  --keys=password -n argocd --to=-
   ```
