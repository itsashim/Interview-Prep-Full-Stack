# Authentication vs Authorization

The fundamental distinction:
Authentication: who are you? identity
Authorization: What can they do?? permissions

## Authentication
It is the process of establishing that a claimed 
identity is genuine.

Suppose the server receives email and password
and now the server has to determine, 
Is this the actual owner of this account?
It might verify: email -> find account -> verify password -> Authentication successfull

after authentication, the server establishes an identity.
this identity can be represented by token or session.

## Authorization
Now suppose the authenticated user requests to delete some resources

the server knows that user is ashim  but it needs to determine if that user
has the permission to delete that resources or not.

## The complete request
                    HTTP Request
                         │
                         ▼
                ┌─────────────────┐
                │ Authentication  │
                └────────┬────────┘
                         │
                    Who are you?
                         │
                         ▼
                    User Identity
                         │
                         ▼
                ┌─────────────────┐
                │ Authorization   │
                └────────┬────────┘
                         │
                 Are you allowed?
                         │
                         ▼
                   Business Logic
                         │
                         ▼
                    Database

