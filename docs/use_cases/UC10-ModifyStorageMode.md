# UC10 - Modify Storage Mode

## Sequence Diagrams

```mermaid
sequenceDiagram
    actor Admin
    participant System
    participant Database

    Admin->>System: Prompt to enter system configuration
    activate System
    Admin->>System: Prompt to enter storage mode configuration
    System-->>Admin: Display current storage mode and available options
    deactivate System

    Admin->>System: Select desired storage method
    activate System

    alt 3a. Selected method is already active
        System-->>Admin: Notify no change needed
    else Selected method is different
        System->>Database: Test connection to selected storage
        activate Database
        Database-->>System: Return connection result
        deactivate Database

        alt 4a. Fail to connect to selected storage
            System-->>Admin: Notify connection failure and rollback to previous method
        else Connection successful
            System-->>Admin: Notify success and apply new storage method
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Alternate between storing data into a PostgreSQL database or a JSON file             |
| **Actor**            | Admin       |
| **Pre-conditions**   | Having an active Admin session |
| **Nominal Scenario** | 1. The Admin prompts to enter the system configuration <br> 2. The Admin prompts to enter storage mode configuration <br> 3. The Admin chooses the desired storage method <br> 4. The system applies and saves the configuration.|
| **Post-conditions**  | The storage method is upadted and persisted |
| **Exceptions**       | 3a. The data storage method is already selected: the Admin is notified and no change is made <br> 4a. Fail to connect to the selected database: the system rollsback to the previous method and notifies the Admin about the failure|
