# UC00 - Login as Admin

## Sequence Diagram

```mermaid
sequenceDiagram
    actor User
    participant System
    participant Database

    User->>System: Prompt to initiate Admin session
    activate System
    System-->>User: Request username and password
    deactivate System

    User->>System: Provide username and password
    activate System
    
    System->>Database: Verify provided credentials
    activate Database
    Database-->>System: Return verification result
    deactivate Database

    alt Credentials are valid
        System-->>User: Elevate to active Admin session
    else 3a. Credentials do not match
        System-->>User: Notify invalid credentials and prompt to try again
    else 3b. System unable to verify credentials
        System-->>User: Notify technical failure and abort login
    end
    deactivate System
```

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Initiate an active Admin session |
| **Actor**            | User |
| **Pre-conditions**   | No active Admin session exists |
| **Nominal Scenario** | 1. The User prompts the system to initiate an Admin session, and the system requests the username and password.<br>2. The User provides the username and password.<br>3. The system verifies the provided credentials with the database.<br>4. The User is elevated to an active Admin session. |
| **Post-conditions** | The User is authenticated as an Admin. |
| **Exceptions**      | 3a. The credentials do not match: the system notifies the User of invalid credentials and prompts them to try again.<br>3b. The system is unable to verify the credentials: the system notifies the User of a technical failure and aborts the login. |
