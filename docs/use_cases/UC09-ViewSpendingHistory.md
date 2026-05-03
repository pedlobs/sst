# UC09 - View Spending History

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to view spending history
    activate System
    System-->>User: Request desired time period
    deactivate System

    User->>System: Provide time period
    activate System

    alt 2a. Time period is invalid
        System-->>User: Notify invalid period and prompt to try again
    else Time period is valid
        System->>Database: Fetch spending history for period
        activate Database
        Database-->>System: Return spending history
        deactivate Database

        alt 3a. Fail to connect to database
            System-->>User: Notify technical failure and cancel operation
        else Fetch successful
            System-->>User: Display spending history
        end
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | View the spending history over a determined period of time |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to see the spending history<br>2. The User prompts the desired time period<br>3. The system retrieves and displays the spending history for the selected time period |
| **Post-conditions**  | The spending history for the selected time period has been displayed |
| **Exceptions**       | 2a. The given period of time is invalid: the User is notified and prompted to try again<br>3a. The system cannot connect to the database: the User is notified and the operation is cancelled |
