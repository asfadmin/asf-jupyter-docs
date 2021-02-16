# Troubleshooting Guide - Deploying OpenSARlab

- [Why don't my Cognito triggers fire my lambdas?](#My-Cognito-Triggers-Don't-Fire-my-Lambdas)

## Why don't my Cognito triggers fire my lambdas?



## Why aren't pods triggering scale-up?
1. Check the Kubernetes version. Scale-up from 0 nodes wasn't added until v1.18
1. If the deployment is new or recently updated, try raising the "desired capacity" of the autoscalers to 1. This will often get things running again.


## Why is the Post Hook failing with a git related error?
Good question

## The BuildJupyterHub stage of the osl-org-maturity-Pipeline CodePipeline fails on the "helm upgrade jupyter jupyterhub/jupyterhub --install ..." call.
Check the helm_config.yaml and confirm the correctness of the hub image tag.


## When I press the "Sign in with AWS Cognito" button, I receive the message "An error was encountered with the requested page."

## Why can't I connect multiple deployments to a single Cognito User Pool?


