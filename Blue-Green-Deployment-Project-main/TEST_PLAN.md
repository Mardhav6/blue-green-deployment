# Blue-Green Deployment Test Plan

## Test Cases

### TC1: Verify Blue and Green Deployments
1. **Objective**: Ensure both blue and green deployments are active in the cluster
2. **Steps**:
   - Deploy blue version
   - Deploy green version
   - Check running pods
3. **Expected Result**:
   - Both blue and green pods should be running
   - Each deployment should have the specified number of replicas
4. **Command**:
   ```bash
   kubectl get pods -l app=portfolio
   ```

### TC2: Service Routing Verification
1. **Objective**: Validate service points to correct color deployment
2. **Steps**:
   - Check current service configuration
   - Verify service selector matches active deployment
3. **Expected Result**:
   - Service selector should match the active deployment color
   - All traffic should be routed to the active deployment
4. **Command**:
   ```bash
   kubectl describe service portfolio-service
   ```

### TC3: Rollback Testing
1. **Objective**: Verify rollback by switching service back to previous version
2. **Steps**:
   - Switch traffic to green deployment
   - Verify traffic routing
   - Switch back to blue deployment
3. **Expected Result**:
   - Traffic should switch smoothly between deployments
   - No downtime during switch
4. **Command**:
   ```bash
   kubectl patch service portfolio-service -p '{"spec":{"selector":{"version":"blue"}}}'
   ```

### TC4: Pipeline Automation
1. **Objective**: Verify automated pipeline builds and deploys on Git push
2. **Steps**:
   - Make a code change
   - Push to GitHub
   - Monitor Jenkins pipeline
3. **Expected Result**:
   - Pipeline should trigger automatically
   - New version should be deployed to inactive environment
4. **Verification**:
   - Check Jenkins build history
   - Verify new deployment in Kubernetes

### TC5: Deployment Health Check
1. **Objective**: Verify Kubernetes deployment rollout status
2. **Steps**:
   - Monitor deployment rollout
   - Check pod health
   - Verify application accessibility
3. **Expected Result**:
   - Deployment should complete successfully
   - All pods should be healthy
   - Application should be accessible
4. **Command**:
   ```bash
   kubectl rollout status deployment/portfolio-blue
   kubectl get pods -l app=portfolio
   ```

## Test Environment Setup
1. **Prerequisites**:
   - Jenkins server running
   - Kubernetes cluster configured
   - GitHub repository with webhook
   - Docker registry access

2. **Test Data**:
   - Sample application code
   - Docker images for both versions
   - Kubernetes manifests

## Test Execution
1. **Pre-test**:
   - Clean up existing deployments
   - Verify cluster state
   - Ensure Jenkins is running

2. **Test Execution**:
   - Execute test cases in sequence
   - Document results
   - Capture any issues

3. **Post-test**:
   - Clean up test resources
   - Document findings
   - Report any issues

## Success Criteria
- All test cases pass
- No downtime during deployment
- Successful rollback capability
- Automated pipeline execution
- Proper traffic routing 