# UC04 - View Subscription Catalog

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to view subscription catalog
    activate System
    
    System->>Database: Fetch all subscriptions
    
    alt 2a. Fail to connect to database
        System-->>User: Notify technical failure and cancel operation
    else Connection successful
        activate Database
        Database-->>System: Return list of subscriptions
        deactivate Database
        System-->>User: Display subscription catalog
    end
    deactivate System
    
    User->>System: Prompt to quit catalog view
    activate System
    System-->>User: Close catalog and return to previous view
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Display every subscription present in the database |
| **Actor**            | User |
| **Pre-conditions**   | The User is authenticated |
| **Nominal Scenario** | 1. The User prompts the system to view the subscription catalog.<br>2. The system queries the database for all subscriptions.<br>3. The system displays the subscription catalog to the User.<br>4. The User prompts to quit the catalog view, and the system closes the catalog. |
| **Post-conditions**  | The User has viewed the subscription catalog. |
| **Exceptions**       | 2a. The system cannot connect to the database: the User is notified and the operation is cancelled. |
