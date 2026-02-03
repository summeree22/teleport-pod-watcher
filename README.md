# Teleport Kubernetes Pod Watcher Extension

This project extends the Teleport open source platform by adding Kubernetes Pod level event monitoring and role based access control, integrated with Teleport roles and external notifications (Slack).

The implementation is based on a fork of the Teleport repository and focuses on enhancing Kubernetes observability and access governance using real cluster sessions rather than dummy or mock clusters.

## 🚀 Key Features
### 1. Kubernetes Pod Event Watcher (client-go)

- Implemented a Kubernetes Pod watcher using client-go

- Detects Pod lifecycle events (create / update / delete)

- Designed to run against real session-based Kubernetes clusters
- Located in:
  ```text
  lib/kube/watcher/watcher.go
  ```

### 2. Pod Label ↔ Teleport Role Matching

- Introduced logic to map Kubernetes Pod labels to Teleport Roles

- Enables fine-grained Pod-level access control

- Access decisions are evaluated dynamically when Pod events occur

- Core logic implemented in:
  ```text
  lib/kube/watcher/match_pod_role.go
  lib/services/role.go
  ```

### 3. Role-Based Access Enforcement

- Extended Teleport’s role service to support Pod access validation

- Determines whether a Teleport role is allowed to access a specific Pod

- Related files:
  ```text
  lib/services/role.go
  lib/services/role_test.go
  ```

### 4. External Notification (Slack Integration)

- Added a notifier module to send real time alerts when:

  -  Unauthorized Pod access is detected

  -  Role Pod matching rules are triggered

- Currently supports Slack Webhook

- Implemented in:
  ```text
  lib/kube/watcher/notifier.go
  ```

### 5. Real Cluster Integration

- Designed to work with:

  -  Minikube

  - Local Kubernetes clusters

  - Externally accessible API servers

- Integrated with Teleport’s session context

- Suitable for real operational environments

## 🧪 Tests & Validation

- Added unit tests for:

- Pod ↔ Role matching logic

  - Role access validation

  - Test coverage ensures safe integration with Teleport core

- Example test files:
  ```text
  lib/kube/watcher/match_pod_role_test.go
  lib/services/role_test.go
  ```

## 📂 Modified / Added Files Summary
```text
lib/
├── kube/
│   └── watcher/
│       ├── watcher.go          # Pod event watcher
│       ├── match_pod_role.go   # Pod ↔ Role matching logic
│       ├── notifier.go         # Slack notification
│       └── *_test.go           # Unit tests
│
├── services/
│   └── role.go                 # Extended role-based Pod access control
│
tool/teleport/common/
└── teleport.go                 # Teleport integration updates
```

## 🎯 Motivation

Teleport provides strong identity-based access control, but Kubernetes access is often namespace or cluster level.

This project explores:

- Pod level security

- Label driven access policies

- Real time visibility into Kubernetes activity

- Operational alerts for security and compliance

## 🛠 Tech Stack

- Go

- Teleport (Open Source)

- Kubernetes client-go

- Minikube / Local K8s

- Slack Webhook

## ✨ What This Demonstrates

- Deep understanding of Teleport internals

- Kubernetes client-go event handling

- Role based access control design

- Open source contribution & extension

- Production oriented thinking (real clusters, alerts, tests)

### ⚠️ Disclaimer

This repository is a personal experimental fork of the Teleport open-source project.
It is not an official Teleport feature and is intended for learning, prototyping, and exploration.
