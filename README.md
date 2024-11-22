### Deploy and Configure ArgoCD
#### This will ensure ArgoCD will automatically keep the Microshift cluster in sync with this repository.
`oc apply -f 0-bootstrap/argocd/setup -n argocd`

`oc apply -k 0-bootstrap/argocd/argocd-instance`


#### Fetch the route and the admin password that was created as part of the ArgoCD deployment
`oc get route -n argocd`

`oc extract secrets/argocd-initial-admin-secret --keys=password -n argocd --to=-`

#### ArgoCD will be accessible from your configured `baseDomain`, example below

`https://microshift-argocd-argocd.apps.microshift.example.com`

#### Utilize the App-of-Apps pattern by deploying a bootstrap ArgoCD Application that references this repository and automatically deploys all applications defined within it using a Kustomization file.

`oc apply -f 0-bootstrap/bootstrap.yaml`

### Example - OKD Console
The OpenShift Console application is included as an example. Deploying this will grant access to the OpenShift web console.

The console doesn't offer the full functionality you might be accustomed to with a complete OpenShift cluster but does provide a user interface for managing Pods, Services, Storage, and more.
