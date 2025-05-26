```
# Step 3: Manual cleanup script (run if needed)
#!/bin/bash
echo "Cleaning up External Secrets resources..."
#
# # Delete the ArgoCD application
kubectl delete application external-secrets -n argocd --wait=true
#
# # Wait for resources to be cleaned up
sleep 30
#
# # Clean up any remaining CRDs (be careful in production!)
kubectl get crd | grep external-secrets | awk '{print $1}' | xargs kubectl delete crd
#
# # Clean up namespace if needed
kubectl delete namespace external-secrets-system --wait=true
#
# # Wait before redeployment
sleep 60
```
