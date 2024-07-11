# Selenium-Docker-Runner

This repository contains the configuration and scripts necessary to run a Selenium Grid with Docker and Docker Compose, specifically tailored for integration with Jenkins pipelines.

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
    docker-compose -f grid.yml up -d
    docker-compose -f test-suites.yml up
    ```

4. After the tests have completed, bring down the Selenium Grid:
    ```sh
    docker-compose -f grid.yml down
    docker-compose -f test-suites.yml down
    ```

### Jenkins Integration

This repository is designed to be integrated with a Jenkins pipeline. Add a link to this repository when creating and configuring a Jenkins pipeline, and everything will work seamlessly, running the tests as expected.

### Docker Compose Configuration

The `docker-compose.yml` file defines the following services:
- `hub`: The Selenium Grid Hub.
- `chrome`: The Selenium Node with Chrome browser.
- `firefox`: The Selenium Node with Firefox browser.
- `vendor-portal`: The test service for the Vendor Portal tests.
- `flight-reservation`: The test service for the Flight Reservation tests.

### Test-Suites | Docker Compose File

```yaml
version: "3"
services:
  vendor-portal:
    image: yehory/selenium-docker
    environment:
      - BROWSER=chrome
      - HUB_HOST=hub
      - THREAD_COUNT=3
      - TEST_SUITE=vendor-portal.xml
    volumes:
      - ./output/vendor-portal:/home/selenium-docker/test-output
  flight-reservation:
    image: yehory/selenium-docker
    environment:
      - BROWSER=firefox
      - HUB_HOST=hub
      - THREAD_COUNT=4
      - TEST_SUITE=flight-reservation.xml
    volumes:
      - ./output/flight-reservation:/home/selenium-docker/test-output
