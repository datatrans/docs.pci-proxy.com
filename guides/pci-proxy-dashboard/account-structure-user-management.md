---
description: Learn more about the PCI Proxy account structure and user management.
---

# Account structure / User management

## Account structure

With PCI Proxy you have one single company account (legal entity) and one single login. Independently of your active subscription plan and test or productive environment. \
\
This company account is called **Contract** and can hold, based on your subscription plan,  one to several sub-accounts (**Projects**). Each **Contract** must contain at least one legally authorized user. Furthermore the invoice is always issued at **Contract** level. \
\
User can be assigned either on **Contract** or **Project** level. Please refer to User management guide below to learn more about the roles and permissions.   

## User management

Navigate to the **Users **menu within the **Contract section** to find the user management.\
\
As the creator of the sandbox account you are automatically assigned with admin permissions for the overall contract. As an admin you are allowed to invite new users to either Contracts or Projects. For each new user you can assign various roles and access rights to them. \
\
Have a look at below mentioned table for detailed user roles. 

**Contract roles**

| Role          | Permission                                                              |
| ------------- | ----------------------------------------------------------------------- |
| Administrator | Full access to contract and project menus. Manage users and edit roles. |
| Write         | Access and modify contract related data                                 |
| Read-only     | Access to contract related data                                         |
| None          | No access rights to contract (enabled by default)                       |

**Project roles (**Assign users to one or several projects)

| Role          | Permission                                                    |
| ------------- | ------------------------------------------------------------- |
| Administrator | Full access to project. Reading & modifying API keys          |
| Write         | Access and modify project related data. No access to API Keys |
| Read-only     | Access to project related data. No access to API Keys         |
| None          | No access rights to projects (enabled by default)             |

****
