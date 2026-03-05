# UC00 - Login as Admin

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Initiate an active Admin session|
| **Actor**            | User        |
| **Pre-conditions**   | No active Admin session existis |
| **Nominal Scenario** | 1. The user prompts the system to initiate an Admin session<br>2. The User provides the username and password<br>3. The system verifies the provided credentials<br>4. The User is elevated to an active Admin session<br> |
| **Post-conditions**  | The Actor is authenticated as Admin |
| **Exceptions**       | 3a. The provided credentials does not match the correct one: the User is notified and prompted to provide the credentials again<br> 3b. The system is unale to verify the login credentials: the system notifies the User of a technical failure and aborts the login process.|
