## Repository Structure

- `Jenkinsfile`: Defines the Jenkins pipeline stages for running and bringing down the Selenium Grid using Docker Compose.
- `docker-compose.yml`: Defines the services for the Selenium Grid Hub, Chrome and Firefox nodes, and the test services.
- `runner.sh`: A shell script executed by the Docker containers to run the tests.

## Getting Started

### Prerequisites

- Docker installed on your machine.
- Docker Compose installed on your machine.
- Jenkins installed and configured with Docker.

### Running the Tests

1. Clone the repository:
    ```sh
    git clone https://github.com/YehorYehorychev/Selenium-Docker-Runner.git
    cd Selenium-Docker-Runner
    ```

2. Ensure that Docker and Docker Compose are installed and running on your machine.

3. Run the Docker Compose to start the Selenium Grid and the test services:
    ```sh
    docker-compose up
    ```

4. After the tests have completed, bring down the Selenium Grid:
    ```sh
    docker-compose down
    ```

### Docker Compose Configuration

The `docker-compose.yml` file defines the following services:
- `hub`: The Selenium Grid Hub.
- `chrome`: The Selenium Node with Chrome browser.
- `firefox`: The Selenium Node with Firefox browser.
- `vendor-portal`: The test service for the Vendor Portal tests.
- `flight-reservation`: The test service for the Flight Reservation tests.
