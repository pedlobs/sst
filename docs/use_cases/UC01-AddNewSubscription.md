# UC01 - Add New Subscription

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Add a new subscription service to the database |
| **Actor**            | User        |
| **Pre-conditions**   | Having the application running |
| **Nominal Scenario** | 1. The User promps the system to add a new subscription service to the database<br>2. The User provides the subscription details (name, category, base value, billing frequency, last billing date, and necessity level)<br>3. The system saves the information to the database and marks the service as active in the database<br> |
| **Post-conditions**  | A new subscription has been added to the database |
| **Exceptions**       | 2a. The provided details are invalid: the User is notified and gets prompted to try again<br> 2b. The User does not add every detail field: the User is notified and prompted to fill the missing fields<br> 3a. The system cannot connect to the database: the user is notified and the operation is cancelled.|
