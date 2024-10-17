# Contributing

This is a personal project for learning and demonstrating Kubernetes observability patterns.

## Making Changes

1. Test changes in a local Kubernetes cluster (minikube, kind, k3s)
2. Validate YAML syntax with `kubectl apply --dry-run=client`
3. Ensure alert rules are valid with `promtool check rules`
4. Update documentation to reflect configuration changes

## Configuration Standards

- Use declarative YAML manifests
- Follow GitOps principles
- Document all resource limits and requests
- Include meaningful labels and annotations
- Store sensitive data in Kubernetes secrets

## Testing

Before applying to production:

```bash
# Validate manifests
kubectl apply --dry-run=client -f .

# Check resource usage
kubectl top nodes
kubectl top pods -n monitoring

# Verify alerts are firing correctly
curl http://prometheus.trebinje.online/prometheus/api/v1/alerts
```
