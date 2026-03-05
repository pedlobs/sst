# UC03 - Remove Subscription

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Removes a subscription service from the database |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User prompts the system to remove a subscription service<br>2.The system executes the View Subscription Catalog use case to display the active subscriptions<br>3. The User writes the name of the desired subscription to remove<br>4. The system applies the changes to the database<br> |
| **Post-conditions**  | A subscription has been removed from the database |
| **Exceptions**       | 3a. The subscription provided does not exists in the database or is invalid: the User is notified and gets prompted to try again<br> 4a. The system cannot connect to the database: the user is notified and the operation is cancelled.|
