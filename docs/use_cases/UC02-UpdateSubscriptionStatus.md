# UC02 - Update Subscription Status

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Changes the subscription status to active or suspended |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to change the satus of a subscription service<br>2.The system executes the View Subscription Catalog use case to display the active subscriptions<br>3. The User writes the name of the desired subscription service update the status<br>4. The User provides the desired subscription status<br>5. The system saves the information to the database |
| **Post-conditions**  | A subscription's status has been altered |
| **Exceptions**       | 2a. The system cannot connectto the database: the User is notified and the operation is cancelled<br>3a. The subscription service name provided does not exist or is invalid: the User is notified and prompted to try again<br>4a. The provided status is invalid: the User is notified and gets prompted to try again<br>5a. The system cannot connect to the database: the User is notified and the operation is cancelled.|
