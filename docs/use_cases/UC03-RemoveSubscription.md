# UC03 - Remove Subscription

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to remove a subscription
    activate System
    rect rgb(230, 230, 230)
        Note over User,Database: ref - UC04: View Subscription Catalog
    end
    System-->>User: Request subscription name
    deactivate System

    User->>System: Provide subscription name
    activate System
    
    System->>Database: Query subscription by name
    
    alt 3a. Fail to connect to database
        System-->>User: Notify technical failure and cancel operation
    else Connection successful
        activate Database
        Database-->>System: Return query result
        deactivate Database
        
        alt Subscription exists
            System->>Database: Delete subscription
            
            alt 4a. Fail to connect to database
                System-->>User: Notify technical failure and cancel operation
            else Deletion successful
                activate Database
                Database-->>System: Confirm deletion
                deactivate Database
                System-->>User: Notify success
            end
        else 3b. Subscription does not exist
            System-->>User: Notify invalid name and prompt to try again
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Remove a subscription service from the database |
| **Actor**            | User |
| **Pre-conditions**   | The User is authenticated and has privileges to remove subscriptions |
| **Nominal Scenario** | 1. The User prompts the system to remove a subscription.<br>2. The system executes UC04: View Subscription Catalog and requests the subscription name.<br>3. The User provides the name, and the system queries the database to verify its existence.<br>4. The system deletes the subscription from the database and notifies the User of success. |
| **Post-conditions**  | A subscription has been permanently removed from the database. |
| **Exceptions**       | 3a. The system cannot connect to the database during verification: the User is notified and the operation is cancelled.<br>3b. The provided subscription name does not exist: the User is notified and prompted to try again.<br>4a. The system cannot connect to the database during the delete operation: the User is notified and the operation is cancelled. |
