# Kubernetes

List of handy commands.

## Common Commands

`kubectl get pods` - get list of pods

`kubectl logs -f pod_name` - get logs for a pod

`kubectl -n namespace rollout restart deployment/name.pod_name` - restart a pod

## Setting Context

### Temporarily for current command only

> Keeps your current context set to local context (or whatever it is currently set to) except for the current command being executed.

`kubectl --context name-of-context get pods` - get pods within specific context

Note: Like in above example, `--context name-of-context` is the key part to use with any command to run it in a specific context for just that command.

### Permanently until a new context is set

> With this method, don't forget to switch back to local context to make sure that you aren't accidentally messing with a shared context unintentionally.

`aws eks --region region-name update-kubeconfig --name last-part-of-name-of-context --alias name-of-context --role-arn role-arn-here`

`kubectl config set-context name-of-context --namespace=name_of_namespace`

## Elasticsearch

`bundle exec name_of_api:transaction_search_populate[01/01/1970,01/10/2030]` - populate an empty ES index

`bundle exec name_of_api:transaction_search_update[01/01/1970,01/10/2030]` - update an existing ES index

Note: Probably doesn't technically matter if populate command is used in place of update command, since ES knows when to create vs. update a document.
