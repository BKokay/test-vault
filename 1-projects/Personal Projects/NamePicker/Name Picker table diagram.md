``` mermaid
erDiagram
    users ||--o{ user_liked_names : "likes"
    names ||--o{ user_liked_names : "liked by"

    users {
        UUID id PK
        VARCHAR(50) email
        VARCHAR(50) oauth_id
        oauth_provider oauth_provider
        TIMESTAMP created_at
        TIMESTAMP last_login
    }

    names {
        UUID id PK
        VARCHAR(50) name
        gender_type gender
        CHAR(1) starts_with
        INTEGER year
        INTEGER popularity
    }

    user_liked_names {
        UUID user_id PK,FK
        UUID name_id PK,FK
        TIMESTAMP liked_at
    }
```