# UC12 - Filter/Sort Subscription Catalog

| Field                | Description |
|----------------------|-------------|
| **Goal**             | Filter or sort the subscription catalog to improve navigation |
| **Actor**            | None (triggered exclusively via <<extend>> from UC04) |
| **Pre-conditions**   | The subscription catalog is being displayed |
| **Nominal Scenario** | 1. The User prompts the system to filter or sort the catalog<br>2. The User provides the desired filter or sorting criteria<br>3. The system retrieves and displays the catalog according to the provided criteria |
| **Post-conditions**  | The subscription catalog has been displayed according to the selected criteria |
| **Exceptions**       | 2a. The provided criteria is invalid: the system notifies the User and prompts them to try again<br>3a. The system cannot retrieve the filtered or sorted catalog: the system notifies the User and displays the unfiltered catalog |
