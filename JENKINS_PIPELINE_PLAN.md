Assignment 2 Jenkins Pipeline 

Checkout Repository 
↓ 
Pytest Execution 
↓ 
SonarQube Analysis 
↓ 
Quality Gate Validation 
↓ 
Docker Image Build 
↓ 
Docker Hub Push 
↓ 
Deployment Validation

Target Assignment 2 CI Pipeline 

GitHub 
↓ 
Checkout Source Code 
↓ 
Pytest Validation 
↓ 
SonarQube Static Analysis 
↓ 
Quality Gate 
↓ 
Docker Build 
↓ 
Docker Hub Push 
↓ 
Deployment Validation

Assignment 2 Quality Pipeline

Checkout Source Code
↓
Pytest Validation
↓
SonarQube Static Analysis
↓
Quality Gate Validation
↓
Build Approval

Quality Gate Rules

- No critical code issues
- No blocker code issues
- Automated tests must pass
- Build proceeds only after quality validation