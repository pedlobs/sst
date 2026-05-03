# UC11 - View Execution Logs

## Sequence Diagram

```mermaid
sequenceDiagram
    actor Admin
    participant System
    participant Database

    Admin->>System: Prompt to enter system configuration
    activate System
    Admin->>System: Prompt to view execution logs
    deactivate System

    System->>Database: Fetch execution logs
    activate Database
    Database-->>System: Return execution logs
    deactivate Database

    alt 3a. No execution logs exist
        System-->>Admin: Notify no logs available and return to system configuration
    else 3b. Fail to connect to database
        System-->>Admin: Notify technical failure and return to system configuration
    else Fetch successful
        System-->>Admin: Display execution logs

        Admin->>System: Prompt to exit logs view
        activate System
        System-->>Admin: Return to system configuration
        deactivate System
    end
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | View the system's execution logs |
| **Actor**            | Admin |
| **Pre-conditions**   | Having an active Admin session|
| **Nominal Scenario** | 1. The Admin prompts to enter system configuration<br>2. The Admin prompts to be shown the execution logs<br>3. The system prints the execution logs on the terminal<br>4. The Admin exits the logs view and returns to the system configuration page |
| **Post-conditions**  | The execution logs are printed on the terminal |
| **Exceptions**       | 3a. There are no execution logs: the Admin is notified and the interface rollsback to the system configuration page<br> 3b. The system cannot fetch the execution logs: the Admin gets notified of the error and the interface rollsback to the system configuration page|
