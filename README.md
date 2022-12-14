# Sample Sonarcloud

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=sample-sonarcloud&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=sample-sonarcloud)

Update your pom.xml file with the following properties:
```
<properties>
  <sonar.projectKey>chance-solutions_sample-gitlab-registry</sonar.projectKey>
  <sonar.organization>chance-solutions</sonar.organization>
</properties>
```

Create or update your `.gitlab-ci.yml`  yaml file with the following content:
```
variables:
  SONAR_USER_HOME: "${CI_PROJECT_DIR}/.sonar"  # Defines the location of the analysis task cache
  GIT_DEPTH: "0"  # Tells git to fetch all the branches of the project, required by the analysis task
sonarcloud-check:
  image: maven:3.6.3-jdk-11
  cache:
    key: "${CI_JOB_NAME}"
    paths:
      - .sonar/cache
  script:
    - mvn verify sonar:sonar
  only:
    - merge_requests
    - master
    - develop
```

Manual run
```
SONAR_TOKEN:*
$ mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dmaven.test.skip=true
```
