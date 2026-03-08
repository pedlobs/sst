# UC01 - Add New Subscription

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to add a new subscription
    activate System
    System-->>User: Request subscription service details
    deactivate System

    User->>System: Provide subscription service details
    activate System
    
    alt 2a. Details are invalid / 2b. Missing fields
        System-->>User: Notify invalid/missing details and prompt to try again
    else Details are valid and complete
        System->>Database: Check if subscription already exists
        activate Database
        
        alt 3a. Fail to connect to database
            System-->>User: Notify technical failure and cancel operation
        else 3b. Subscription already exists
            Database-->>System: Return existing record
            System-->>User: Notify duplicate service and prompt to modify
        else Subscription is unique
            Database-->>System: Return no matches
            System->>Database: Save new subscription details
            
            alt 4a. Fail to connect to database during save
                System-->>User: Notify technical failure and cancel operation
            else Save successful
                Database-->>System: Confirm save
                deactivate Database
                System-->>User: Notify success
            end
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Add a new subscription service to the database |
| **Actor**            | User |
| **Pre-conditions**   | The User is authenticated and has privileges to add subscriptions |
| **Nominal Scenario** | 1. The User prompts the system to add a new subscription service.<br>2. The system requests the subscription details.<br>3. The User provides the details (name, category, base value, billing frequency, last billing date, and necessity level).<br>4. The system verifies the data and checks the database to ensure the subscription does not already exist.<br>5. The system saves the information and marks the service as active in the database. |
| **Post-conditions**  | A new subscription has been added to the database. |
| **Exceptions**       | 2a. The provided details are invalid: the User is notified and prompted to try again.<br>2b. The User is missing required fields: the User is notified and prompted to fill the missing fields.<br>3a / 4a. The system cannot connect to the database: the User is notified and the operation is cancelled.<br>3b. A subscription with the provided name already exists: the User is notified of the duplicate and prompted to modify the details. |
