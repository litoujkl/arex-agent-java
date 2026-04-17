# Development Environment Setup (Cursor Cloud VM)

This repository was validated in a Linux cloud VM with JDK 21.

## Prerequisites

- Java (JDK 8+ supported by this project; validated with JDK 21)
- Maven

Install Maven on Ubuntu/Debian:

`sudo apt-get update && sudo apt-get install -y maven`

## Verified Commands

Run from repository root:

1. Verify toolchain

`java -version`

`mvn -version`

2. Build all modules

`mvn clean install -DskipTests`

3. Run packaged artifacts to verify runtime

`java -jar arex-integration-tests/arex-main-integration-test/target/arex-main-integration-test.jar`

`java -jar arex-attacher/target/arex-attacher.jar 9999999 arex-agent/target/arex-agent.jar`

The `arex-attacher` command above is a sanity run that confirms execution; it is expected to print an error for a non-existent PID (`No such process`) while still proving runtime wiring works.

## Notes

- Main project build guidance in the repository root README remains the canonical source:
  - `mvn clean install -DskipTests`
  - `mvn clean install -DskipTests -Pjar-with-version`
