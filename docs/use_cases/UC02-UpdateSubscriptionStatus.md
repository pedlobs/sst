# UC02 - Update Subscription Status

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to update a subscription status
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
            System-->>User: Request new status
            deactivate System
            
            User->>System: Provide new status
            activate System
            
            alt Status is valid
                System->>Database: Save new status
                
                alt 5a. Fail to connect to database
                    System-->>User: Notify technical failure and cancel operation
                else Save successful
                    activate Database
                    Database-->>System: Confirm save
                    deactivate Database
                    System-->>User: Notify success
                end
            else 4a. Status is invalid
                System-->>User: Notify invalid status and prompt to try again
            end
        else 3b. Subscription does not exist
            System-->>User: Notify invalid name and prompt to try again
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Change the subscription status to active or suspended |
| **Actor**            | User |
| **Pre-conditions**   | The User is authenticated and has privileges to update subscriptions |
| **Nominal Scenario** | 1. The User prompts the system to update a subscription status.<br>2. The system executes UC04: View Subscription Catalog and requests the subscription name.<br>3. The User provides the name, and the system queries the database to verify its existence.<br>4. The system requests the new status, and the User provides it.<br>5. The system validates the status and saves the update to the database. |
| **Post-conditions**  | A subscription's status has been updated. |
| **Exceptions**       | **3a.** The system cannot connect to the database during verification: the User is notified and the operation is cancelled.<br>**3b.** The subscription does not exist: the User is notified and prompted to try again.<br>**4a.** The provided status is invalid: the User is notified and prompted to try again.<br>**5a.** The system cannot connect to the database during the save operation: the User is notified and the operation is cancelled. |
