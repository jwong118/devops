Installing Kyverno Policy Helm Chart
 # helm install kyverno-policies --namespace kyverno kyverno/kyverno-policies

View Kyverno Policies Applied On Cluster
# kubectl get clusterpolicy

Deleting a Kyverno Policy
- Using the policy name:
  # kubectl delete clusterpolicy -name <policy-name>
- Using the object configuration file (YAML file) that was used to create the policy.
  # kubectl delete -f <policy_file.yaml>
- Delete all the cluster policies
  # kubectl delete cpol --all