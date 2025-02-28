# OpenRewrite and Moderne Integration testing

In this repo I try to establish tests that can help OpenRewrite and Moderne to archive a more stable UX/DX for releases.
Main goal is to cover the very unpleasant "did they even started this thing once?" situations. 

## Tool under Test

- OpenRewrite Gradle Plugin
- OpenRewrite Maven Plugin
- Moderne CLI
- OpenRewrite/rewrite-Spring
- Moderne/rewrite-Spring
- maybe Moderne SaaS as Repository

## Test Cases

### OpenRewrite and OSS CLI ✅

All Testcases are run against the [openrewrite/spring-petclinic-migration](https://github.com/openrewrite/spring-petclinic-migration) repository form the branch 2.1.x, which contains the Spring Boot PetClinic sample using Spring Boot 2.1.x.
Each test is run with Maven and Gradle Plugin from Maven Central.

**Testcase:**
1. clone openrewrite/spring-petclinic-migration branch 2.1.x
2. run OpenRewrite integration on the fly with recipe Spring Boot Migration 3.3

| Integration vs. rewrite-spring | Latest Release | Latest Snapshot  |
|--------------------------------|----------------|------------------|
| Latest Release/Stable          | baseline       | same as baseline |
| Latest Snapshot/Staging        | no failure     | no failure       |

See actions for martix jobs for above combinations of [Gradle](.github/workflows/integration-test-gradle.yml), [Maven](.github/workflows/integration-test-maven.yml) and [Mod CLI JAR](.github/workflows/integration-test-maven.yml) 

### Moderne CLI / SaaS ❌

All Testcases are run against an organization consisting of a Spring Boot Project.

**Testcase:**
1. load Moderne CLI
2. activate Moderne CLI
3. load moderne/rewrite-spring recipes
4. clone the Spring Boot Project via Mod CLI
5. build LST
6. run Moderne CLI with recipe Spring Boot Migration 3.4

| CLI vs. rewrite-spring | Latest Release | Latest Snapshot  |
|------------------------|----------------|------------------|
| Stable                 | baseline       | same as baseline |
| Staging                | no failure     | no failure       |

### Future Plan 🔭

- [ ] Store a LST created with the last Release and check if current Stable/Staging can read/migrate this LST
