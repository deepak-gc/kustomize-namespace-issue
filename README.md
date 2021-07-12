 ### Kustomize - Create multi and single deployment using same namespace

 Kustomize directory structure 
```
├── base
│   ├── deployment.yaml
│   └── kustomization.yaml
└── overlays
    └── prod
        ├── kustomization.yaml
        ├── namespace-a
        │   ├── deployment-a1
        │   │   ├── kustomization.yaml
        │   │   └── patch.yaml
        │   ├── deployment-a2
        │   │   ├── kustomization.yaml
        │   │   └── patch.yaml
        │   ├── kustomization.yaml
        │   └── namespace.yaml
        ├── namespace-b
        │   ├── deployment-b1
        │   │   ├── kustomization.yaml
        │   │   └── patch.yaml
        │   ├── deployment-b2
        │   │   ├── kustomization.yaml
        │   │   └── patch.yaml
        │   ├── kustomization.yaml
        │   └── namespace.yaml
        └── namespace-c

```

As you can see above, I have `prod` environment with `namesapce-a` and `namespace-b` and few more.
To  create deployment for all, I can simply run the below command: 

```
    > kustomize overlays/prod
```
Which works flawlessly, both namespaces are created along with other deployment files for all deployments.  

To create a deployment for only namespace-a: 

```
    > kustomize overlays/prod/namespace-a
```

That also works. :) 

But that's not where the story ends for me at-least.

I would like to keep the current functionality and be able to deploy `deployment-a1, deployment-a2 ...`

```
    > kustomize overlays/prod/namespace-a/deployment-a1
```

If I put the namespace.yaml inside `deployment-a1` folder and add it in `kustomization.yaml`
then the above command works but previous 2 fails with error because now we have 2 namespace files with same name. 

I have 2 queries. 

1. Can this directory structure be improved?    
2. How can I create namesapce with single deployment without breaking the other functionality?

