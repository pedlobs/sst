# UC08 - Log Payment

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to log a payment
    activate System
    rect rgb(230, 230, 230)
        Note over User,Database: ref - UC04: View Subscription Catalog
    end
    System-->>User: Request subscription name
    deactivate System

    User->>System: Provide subscription name
    activate System

    System->>Database: Query subscription by name
    activate Database
    Database-->>System: Return query result
    deactivate Database

    alt 3a. Subscription does not exist
        System-->>User: Notify invalid name and prompt to try again
    else Subscription exists
        System-->>User: Request payment method
        deactivate System

        User->>System: Provide payment method
        activate System

        alt 4a. Payment method is invalid
            System-->>User: Notify invalid method and prompt to try again
        else 4b. Payment method does not exist
            rect rgb(230, 230, 230)
                Note over User,Database: <<extend>> UC07: Register Payment Method
            end
            System->>Database: Save payment and update last billing date
            activate Database
            Database-->>System: Confirm save
            deactivate Database
            System-->>User: Notify success
        else Payment method exists
            System->>Database: Save payment and update last billing date
            activate Database
            Database-->>System: Confirm save
            deactivate Database
            System-->>User: Notify success
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Register a new payment for a subscription service |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to register a new payment for a subscription service<br>2. The system executes the View Subscription Catalog use case to display the active subscriptions<br>3. The User selects the subscription service for which to register a payment<br>4. The User selects the payment method used for the payment<br> \<\<extend\>\> [if new payment method needed]: UC07 - Register Payment Method<br>5. The system saves the information to the database and updates the subscription's last billing day |
| **Post-conditions**  | A new payment has been added to the log list of previous payments and the subscription's last billing day has been updated |
| **Exceptions**       | 3a. The subscription service name provided does no exist in the database or is invalid: the User is notified and prompted to try again<br>4a. The payment method provided is invalid: the User is notified and prompted to try again<br>5a. The system cannot connect to the database: the User is notified and the operation is cancelled<br> |
