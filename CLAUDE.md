# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

`phodam` is a freshly generated Spring Initializr skeleton: a single `@SpringBootApplication` class (`com.example.phodam.PhodamApplication`) and a context-load test. There is no domain code, persistence layer, or configuration beyond `spring.application.name` yet. The directory is not a git repository yet.

## Stack

- Kotlin 2.3.21 on JVM toolchain 21, Gradle 9.8.1 (Kotlin DSL, wrapper included)
- Spring Boot 4.1.1 with `spring-boot-starter-webmvc` (servlet stack, not WebFlux)
- Jackson 3 (`tools.jackson.module:jackson-module-kotlin`). The package is `tools.jackson.*`, not `com.fasterxml.jackson.*`
- Tests: JUnit 5 via `kotlin-test-junit5` and `spring-boot-starter-webmvc-test`
- Compiler flags: `-Xjsr305=strict` (Spring nullability annotations are enforced as Kotlin types) and `-Xannotation-default-target=param-property`
- The `kotlin("plugin.spring")` plugin makes Spring-annotated classes `open` automatically, so you don't need to add `open` by hand

## Commands

```bash
./gradlew bootRun                     # run the app (default port 8080)
./gradlew build                       # compile + test + package
./gradlew test                        # all tests
./gradlew test --tests 'com.example.phodam.PhodamApplicationTests'            # single class
./gradlew test --tests 'com.example.phodam.PhodamApplicationTests.contextLoads' # single method
./gradlew bootJar                     # executable jar in build/libs/
./gradlew bootBuildImage              # OCI image
```

No linter or formatter (ktlint/detekt) is configured. Existing sources use tab indentation.
