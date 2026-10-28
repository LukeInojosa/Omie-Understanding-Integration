# Omie-Understanding-Integration
Repositório para documentar sistema Omie a fim realizar integração

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER {
        int id PK
        string name
        string email
    }
    ORDER ||--|{ ORDER_ITEM : contains
    ORDER {
        int id PK
        int customer_id FK
        datetime order_date
    }
    PRODUCT ||--o{ ORDER_ITEM : "ordered in"
    PRODUCT {
        int id PK
        string title
        decimal price
    }
    ORDER_ITEM {
        int order_id PK,FK
        int product_id PK,FK
        int quantity
    }
```
