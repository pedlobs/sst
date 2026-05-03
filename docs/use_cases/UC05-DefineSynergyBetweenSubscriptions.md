# UC05 - Define Synergy Between Subscriptions 

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to define a synergy between subscriptions
    activate System
    rect rgb(230, 230, 230)
        Note over User,Database: ref - UC04: View Subscription Catalog
    end
    System-->>User: Request source and target subscription names
    deactivate System

    User->>System: Provide source subscription name
    activate System

    System->>Database: Query source subscription by name
    activate Database
    Database-->>System: Return query result
    deactivate Database

    alt 3a. Source subscription does not exist
        System-->>User: Notify invalid name and prompt to try again
    else Source subscription exists
        System-->>User: Request target subscription name
        deactivate System

        User->>System: Provide target subscription name
        activate System

        System->>Database: Query target subscription by name
        activate Database
        Database-->>System: Return query result
        deactivate Database

        alt 4a. Target subscription does not exist
            System-->>User: Notify invalid name and prompt to try again
        else Target subscription exists
            System-->>User: Request synergy discount value
            deactivate System

            User->>System: Provide discount value
            activate System

            alt 5a. Discount format is invalid
                System-->>User: Notify invalid format and prompt to try again
            else Discount is valid
                System->>Database: Save synergy
                activate Database
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
| **Goal**             | Establishes a relation between two different subscription services |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to establish a relation between two subscription services<br>2.The system executes the View Subscription Catalog use case to display the active subscriptions<br>3. The User writes the name of the subscription service that causes a synergy<br>4.The User writes the name of the subscription service that benefits from the first subscription service<br>5. The User adds the discount associated, which can be a flat value or a percentage<br>6. The system saves the information to the database<br>|
| **Post-conditions**  | A synergy between two subscription services is added|
| **Exceptions**       | 3a. The prompted subscription service does not exist in the database: the user is notified and the User is prompted to try again<br>4a. The prompted subscription service does not exist in the database: the user is notified and the User is prompted to try again<br>5a.The discount has an invalid format: the User is notified and prompted to try again<br>6a.The system cannot connect to the database: the user is notified and the operation is cancelled.|
