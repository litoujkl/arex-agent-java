# AGENTS.md

## Cursor Cloud specific instructions

### Overview
This is **arex-agent-java**, a Java bytecode instrumentation agent for regression testing with real-world production data. It is a library/agent JAR (not a standalone runnable service). The build produces `arex-agent.jar` in `arex-agent-jar/`.

### Prerequisites
- **Java 21** (JDK already available in the VM; project targets Java 8 source/target but builds and tests on JDK 21 per CI)
- **Apache Maven 3.9.x** installed at `/opt/apache-maven-3.9.6` with symlink at `/usr/local/bin/mvn`

### Key commands
| Task | Command |
|------|---------|
| Build (skip tests) | `mvn --batch-mode --no-transfer-progress clean install -DskipTests` |
| Run unit tests | `mvn --batch-mode --no-transfer-progress clean test` |
| Build with version suffix | `mvn clean install -DskipTests -Pjar-with-version` |

### Non-obvious notes
- There is no lint command or standalone linter configured; code quality checks run via SonarCloud in CI only.
- Integration tests under `arex-integration-tests/` require Testcontainers (Docker). They are skipped during normal `mvn test` because their test classes are not triggered by surefire defaults. Running them locally requires Docker.
- The `maven-surefire-plugin` is configured with JDK 21 `--add-opens` flags for module access; tests must run on JDK 9+ (CI uses JDK 21).
- The project uses Maven CI Friendly Versions (`${revision}` property, currently `0.4.8`) and the `flatten-maven-plugin`.
- Build output artifact: `arex-agent-jar/arex-agent.jar` (~23 MB).
- This is a library, not a runnable application. There is no `main` class or dev server to start. The "hello world" validation is a successful build + passing unit tests + verifying the agent JAR is produced.
