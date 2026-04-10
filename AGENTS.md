# AGENTS.md

## Cursor Cloud specific instructions

### Project overview

AREX Agent Java is a bytecode instrumentation agent (not a runnable application). It produces `arex-agent.jar` which attaches to Java applications via `-javaagent`. The repo is a Maven multi-module project (52 modules).

### Prerequisites

- **JDK 21** (pre-installed on the VM; project compiles to Java 8 target)
- **Apache Maven 3.8+** (installed via `sudo apt-get install -y maven`)

### Key commands

| Task | Command |
|------|---------|
| Build (skip tests) | `mvn --batch-mode --no-transfer-progress clean install -DskipTests` |
| Run all unit tests | `mvn --batch-mode --no-transfer-progress test` |
| Build + tests | `mvn --batch-mode --no-transfer-progress clean test verify` |
| Test single module | `mvn --batch-mode test -pl arex-agent-core` |

### Build output

After `mvn install`, the agent JAR is at `arex-agent-jar/arex-agent.jar` (also at `arex-agent/target/arex-agent.jar`).

### Important notes

- The project uses **Maven CI Friendly Versions** (`${revision}` property in root POM, currently `0.4.8`).
- The surefire plugin adds `--add-opens` JVM flags for JDK 17+ module system compatibility. These are already configured in the root POM.
- Unit tests run in **parallel** via JUnit Jupiter parallel execution (configured in root POM surefire plugin).
- Integration tests (`arex-integration-tests/`) require **Docker** (Testcontainers). They are separate from unit tests and will be skipped without Docker. Unit tests work without Docker.
- There is no lint tool configured (no Checkstyle/SpotBugs/PMD). Code style is not enforced by tooling.
- There is no Maven wrapper (`mvnw`) in this repo; system Maven is required.
