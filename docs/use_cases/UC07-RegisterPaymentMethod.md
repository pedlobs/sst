# UC07 - Register Payment Method

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to register a new payment method
    activate System
    System-->>User: Request payment method name
    deactivate System

    User->>System: Provide payment method name
    activate System

    alt 2a. Payment method name is invalid
        System-->>User: Notify invalid name and prompt to try again
    else Name is valid
        System->>Database: Save payment method
        activate Database
        Database-->>System: Confirm save
        deactivate Database
        System-->>User: Notify success
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Register a new payment method to be used when logging in a payment |
| **Actor**            | User        |
| **Pre-conditions**   | 1. Having the application running<br>2. May be triggered from UC08 if the User wants to register a new payment method during a payment log |
| **Nominal Scenario** | 1. The User prompts the system to add a new payment method<br>2. The User writes the name of the new payment method<br>3. The system saves the information to the database |
| **Post-conditions**  | A new payment method has been added to the list of possible payment methods |
| **Exceptions**       | 2a. The payment method name provided is invalid: the User is notified and prompted to try again<br>3a. The system cannot connect to the database: the User is notified and the operation is cancelled<br> |
