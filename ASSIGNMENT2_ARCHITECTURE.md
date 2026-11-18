# ACEest Fitness Gym Assignment 2 Architecture

## CI Pipeline

GitHub
↓
Jenkins
↓
Pytest
↓
SonarQube
↓
Docker Build
↓
Docker Hub Push

## CD Pipeline

Docker Hub
↓
Kubernetes
↓
Rolling Update
↓
Blue-Green Deployment
↓
Canary Deployment
↓
Rollback

## Branch Strategy

main

version-1.0
version-1.1
version-1.1.2
version-2.0.1
version-2.1.2
version-2.2.1
version-2.2.4
version-3.0.1
version-3.1.2
version-3.2.4

release-1.0

feature-sonarqube
feature-dockerhub
feature-kubernetes
feature-bluegreen
feature-canary
feature-shadow
feature-ab-testing
feature-rolling-update
feature-rollback