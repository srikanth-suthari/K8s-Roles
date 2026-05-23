# K8s-Roles

### RBAC - Role Based Access Control

#### This comes under K8s Adminstration

- Using this we provide the required access to the users or groups (group of users)

- In K8s we have some verbs to perform on resources
    - verbs are known as actions like create, read, update, delete etc
    - these can be performed on the resources we have in k8s
    - which are pod, deployment, statefulset, services, secrets and configmaps etc

- In K8s we have 4 types of objects in RBAC, they are
    - Role - namdspace level
    - RoleBinding - To attach the role and user or group
    - ClusterRole - Cluster Level or Non Namespaced
    - ClusterRoleBinding - To attach the clusterrole and user or gruoup

- Roles: Define a set of permissions within a namespace.
- RoleBindings: Associate roles with users, groups, or service accounts within a namespace.
- ClusterRoles: Similar to roles, but apply across the entire cluster.
- ClusterRoleBindings: Associate cluster roles with users, groups, or service accounts across the entire cluster.

- We give role permissions to users or groups based on their "Role"
    - Developer - CRUD Permissions
    - Admin - Read, Update and Delete permissions
    - User - Read/Describe, List etc

### Process of RBAC - Namespace Level

- User --> Role --> RoleBinding

    - Here we are making use of AWS IAM for authentication and authorisation as user management
    - Create a user in AWS IAM and give him the required access like "Describing the EKS Cluster" [with CLI Access]
    - Then create role in K8s with A "RoleName" using Role object
    - Attach the Role to the user with "RoleBinding" object.

* Here we use aws-auth configmap for authentication between AWS IAM and AWS EKS (This is the main step)

    - Update the config file in EKS cluster which is - ".kube/config"

### Process for RBAC - Cluster Level

- User --> ClusterRole --> ClusterRoleBinding

    - Here we are making use of AWS IAM for authentication and authorisation as user management
    - Create a user in AWS IAM and give him the required access like "Describing the EKS Cluster" [with CLI Access]
    - Then create role in K8s with A "ClusterRoleName" using ClusterRole object like resources SC, PV, PVC etc.
    - Attach the Role to the user with "ClusterRoleBinding" object.

* Here we use aws-auth configmap for authentication between AWS IAM and AWS EKS (This is the main step)

    - Update the config file in EKS cluster which is - ".kube/config"

### Service Accounts

- Service accounts in Kubernetes are meant to provide an identity for processes that run in a Pod.

#### OIDC - OpenID Connect
- This requires an authentication system like OIDC (OpenID Connect) to connect the K8s cluster with AWS IAM.
- OpenID Connect (OIDC): This is the modern, widely adopted version (based on OAuth 2.0) that standardizes how identity is verified across web, mobile, and APIs.

- Identity Provider (IdP): Companies like Google, Microsoft, or Apple act as IdPs, confirming to a website that you are who you claim to be.
- How it works: You click "Sign in with..." on a site, authenticate with your provider, and they share an encrypted token with the site to log you in.
- Single Sign-On (SSO): Log into multiple sites with one account.
- Improved Security: No need for websites to store passwords, reducing the impact of data breaches.

- process behind attaching a policy and roles to the service account and a pod

- pod -> service account -> roles -> IAM policies -> the end resource like Secrets Manager in AWS
- here we are creating the service account with command and attaching the roles to it with commands only.
- to create service account using command is:
    * kubectl create sa <service accoutn name> -n <namespace>

- we can create a service account within k8s and attach it with a role and bind the service to a pod for accessing.
- but, if we use the AWS IAM for authentication we need to create a role in aws roles and attach with appropriate policies and  permissions to it
- then we need to attach the role to a service account which is there in our k8s cluster and finally attach the service account to a pod for accessibility
- for this external communication or authentication and authorization with aws from k8s cluster, The OIDC plugin is mandatory for the communication

- * we can do this process with CLI commands and also with K8s yaml manifests