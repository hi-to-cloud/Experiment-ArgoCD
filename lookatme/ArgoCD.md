## ArgoCD 
#### GITOPS
```
- Hari Deploy change to Cluster.
- Cluster Down: After 'X' days, What change made on cluster?
- No tracking, No versining, No auditing.
```
```
- Git as Single Source of truth to deliver applications and infrastructure.

Source code:
- PR with Reviews & Approvals to get final version of code.

- CI: source code: Tracking with Git.
- CD: deployment: Tracking with Git.
```

#### Principles GitOps
```
- Declarative (
    desired state need to be expressed declaratively.
)
- Versioned & immutable (
    desired state stored with versioning, immutability, have entire history.
)
- Pulled Automatically (
    desired state can be pulled by software agents.
)
- Continously Reconciled (
    if we change configuration manually inside cluster it will not allow.
)
```
#### Advantages of GitOps
```
- security (only argocd will deploy applications)
- versioning (track of changes)
- auto upgrades (either pull or push)
- auto healing
- continously reconciled
```

#### Architecture of ArgoCD
```
GitOps -- Sync b/w git & k8s cluster

1. argocd-repo-server - connect to git & get the state
2. argocd-application-controller - connect to k8s & get the state
3. argocd-server - ui & cli
4. argocd-dex-server(proxy server) - api-server integrate Authentication: LDAP, SSO, OIDC
5. argocd-redis - caching
```

#### is GitOps simple?
```
Is it that simple ?
Not actually ....
If Git is single source truth, how to handle the entries by admission controllers ?
For example, you deployed a pod using gitops on the cluster but there is a admission controller that adds resource requests and limits, so should those be removed because as per GitOps, GIT is single source of truth.
- By default, GitOps tools (e.g., ArgoCD, Flux) any changes made outside Git (e.g., by an admission controller) may be reverted
- Admission controllers add complexity but can be handled by syncing manifests properly.

You like GitOps and decided to onboard GitOps with some applications. But what happens to existing resource on your kubernetes cluster ? Will they be deleted is single source of truth.
- By default, GitOps tools (e.g., ArgoCD, Flux) detect drift and may delete unmanaged resources if pruning is enabled.
- Existing resources won’t be deleted if you use adoption strategies like ArgoCD’s app adopt or disable pruning.
```
