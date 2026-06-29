# Maven Basic Commands

Maven is a powerful build automation and dependency management tool widely used in Java development.
This document provides a comprehensive list of essential Maven commands for development, CI/CD, and DevOps workflows.

---

## Setup & Configuration

Basic commands and configurations to initialize Maven projects and verify installation.

| Command                    | Description                          |
| -------------------------- | ------------------------------------ |
| `mvn -version`             | Check Maven version                  |
| `mvn archetype:generate`   | Generate a project from an archetype |
| `mvn help:system`          | Display system properties            |
| `mvn help:active-profiles` | Show active profiles                 |

---

## Project Lifecycle

Commands related to Maven lifecycle phases for building and validating projects.

| Command        | Description                            |
| -------------- | -------------------------------------- |
| `mvn validate` | Validate the project structure         |
| `mvn compile`  | Compile source code                    |
| `mvn test`     | Run tests                              |
| `mvn package`  | Package into JAR/WAR                   |
| `mvn verify`   | Verify integration tests               |
| `mvn install`  | Install artifact into local repository |
| `mvn deploy`   | Deploy artifact to remote repository   |

---

## Cleaning

Commands to clean build artifacts and caches.

| Command                                 | Description                        |
| --------------------------------------- | ---------------------------------- |
| `mvn clean`                             | Remove build folder (`target/`)    |
| `mvn clean install`                     | Clean then install                 |
| `mvn dependency:purge-local-repository` | Remove and re-resolve dependencies |

---

## Running Applications

Commands for running Java applications including Spring Boot.

| Command               | Description                               |
| --------------------- | ----------------------------------------- |
| `mvn exec:java`       | Run main class                            |
| `mvn spring-boot:run` | Run Spring Boot project                   |
| `mvn tomcat7:run`     | Run on embedded Tomcat (if plugin exists) |

---

## Dependency Management

Commands to inspect, resolve, and manage dependencies.

| Command                            | Description                            |
| ---------------------------------- | -------------------------------------- |
| `mvn dependency:tree`              | Show dependency hierarchy              |
| `mvn dependency:list`              | List dependencies                      |
| `mvn dependency:analyze`           | Analyze unused/undeclared dependencies |
| `mvn dependency:resolve`           | Resolve dependencies                   |
| `mvn dependency:copy-dependencies` | Copy dependencies to folder            |

---

## Repository Operations

Commands used to deploy or upload artifacts to remote repositories (Nexus/Artifactory).

| Command                  | Description                      |
| ------------------------ | -------------------------------- |
| `mvn deploy`             | Deploy to configured remote repo |
| `mvn deploy:help`        | Help for deployment plugin       |
| `mvn deploy:deploy-file` | Deploy external JAR manually     |

---

## Profiles

Commands to build and run projects with Maven profiles.

| Command                    | Description                |
| -------------------------- | -------------------------- |
| `mvn install -P<profile>`  | Use specified profile      |
| `mvn test -Pdev`           | Run tests with dev profile |
| `mvn help:active-profiles` | Show active profiles       |

---

## Plugin Management

Commands to work with Maven plugins.

| Command                       | Description                         |
| ----------------------------- | ----------------------------------- |
| `mvn help:effective-pom`      | Show resolved POM including plugins |
| `mvn help:effective-settings` | Show final settings.xml             |
| `mvn plugin:help`             | Help for plugin commands            |
| `mvn plugin:info`             | View plugin info                    |

---

## Test Operations

Commands for running and filtering tests.

| Command                              | Description              |
| ------------------------------------ | ------------------------ |
| `mvn test`                           | Run all tests            |
| `mvn -Dtest=TestClass test`          | Run specific test class  |
| `mvn -Dtest=TestClass#method test`   | Run specific test method |
| `mvn -DskipTests package`            | Skip tests but compile   |
| `mvn -Dmaven.test.skip=true package` | Skip compiling tests     |

---

## Versioning & Release Management

Commands used for tagging and preparing versions using Maven Release Plugin.

| Command                               | Description                 |
| ------------------------------------- | --------------------------- |
| `mvn release:prepare`                 | Prepare project for release |
| `mvn release:perform`                 | Perform release deployment  |
| `mvn versions:set -DnewVersion=x.y.z` | Update project version      |
| `mvn versions:commit`                 | Commit changed versions     |
| `mvn versions:revert`                 | Revert version changes      |

---

## Archetypes (Project Templates)

Commands for generating standard project structures.

| Command                                                      | Description                     |
| ------------------------------------------------------------ | ------------------------------- |
| `mvn archetype:generate`                                     | Generate project from archetype |
| `mvn archetype:generate -DgroupId=com.app -DartifactId=demo` | Generate with properties        |

---

## Inspect & Debug

Commands to inspect, debug, and troubleshoot build issues.

| Command                         | Description                             |
| ------------------------------- | --------------------------------------- |
| `mvn -X`                        | Debug mode with logs                    |
| `mvn --fail-at-end`             | Continue build but show failures at end |
| `mvn --fail-never`              | Never fail build                        |
| `mvn --fail-fast`               | Stop on first failure                   |
| `mvn dependency:tree -Dverbose` | Detailed dependency tree                |

---

## Useful Additional Flags

```bash
-DskipTests            # Skip test execution
-Dmaven.test.skip=true # Skip test compilation
-Pprofile              # Activate a profile
-T 1C                  # Use one thread per CPU core
-o                     # Offline mode
-U                     # Force snapshot update
```

---

## Typical CI/CD Pipeline Example

```bash
mvn clean
mvn compile
mvn test
mvn package
mvn install
mvn deploy
```

