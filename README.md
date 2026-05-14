# K8s-Roles

RBAC - Role Based Access Control    -   This comes under K8s Adminstration

- Using this we provide the required access to the users or groups (group of users)

- In K8s we have some verbs on resources to perform
    - verbs are known as actions like create, read, update, delete etc
    - this can be performed on the resources we have in k8s
    - which are pod, deployment, statefulset, services, secrets and configmaps etc

- In K8s we have 4 types of objects in RBAC, they are
    - Role - namdspace level
    - RoleBinding -
    - ClusterRole - Cluster Level
    - ClusterRoleBinding -

- We give role permissions to users or groups based on their "Role"
    - Developer - CRUD Permissions
    - Admin - Read, Update and Delete permissions
    - User - Read/Describe, List etc

### Process of RBAC

- User --> Role --> RoleBinding