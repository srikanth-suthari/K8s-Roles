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
    - RoleBinding -
    - ClusterRole - Cluster Level
    - ClusterRoleBinding -

* Role - A Role is a collection of permissions that allow users to perform specific actions (verbs, such as “get”, “create”, “and “delete”) on a defined set of Kubernetes resource types (such as Pods, Deployments, and Namespaces).


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
