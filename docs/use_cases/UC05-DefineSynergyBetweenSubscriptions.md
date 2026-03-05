# UC05 - Define Synergy Between Subscriptions 

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Establishes a relation between two different subscription services |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to establish a relation between two subscription services<br>2.The system executes the View Subscription Catalog use case to display the active subscriptions<br>3. The User writes the name of the subscription service that causes a synergy<br>4.The User writes the name of the subscription service that benefits from the first subscription service<br>5. The User adds the discount associated, which can be a flat value or a percentage<br>6. The system saves the information to the database<br>|
| **Post-conditions**  | A synergy between two subscription services is added|
| **Exceptions**       | 3a. The prompted subscription service does not exist in the database: the user is notified and the User is prompted to try again<br>4a. The prompted subscription service does not exist in the database: the user is notified and the User is prompted to try again<br>5a.The discount has an invalid format: the User is notified and prompted to try again<br>6a.The system cannot connect to the database: the user is notified and the operation is cancelled.|
