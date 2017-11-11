# Android CI [![Android CI on Docker Hub](https://img.shields.io/docker/automated/javiersantos/android-ci.svg)](https://store.docker.com/community/images/javiersantos/android-ci)
### Continous Integration (CI) for Android apps on GitLab / Bitbucket
An image for building Android apps with support for multiple SDK Build Tools. This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool. Based on [jangrewe/gitlab-ci-android](https://github.com/jangrewe/gitlab-ci-android).

## Available images
### javiersantos/android-ci:latest
Includes the latest SDK Build Tools and SDK Platform.

* Build Tools: 26.0.2
* Platform: Android 25, 26 & 27
* Android Support: Constraint Layout 1.0.2 & Constraint Layout Solver 1.0.2

## Sample usages
### GitLab
*.gitlab-ci.yml*

```yml
image: javiersantos/android-ci:latest

before_script:
    - export GRADLE_USER_HOME=`pwd`/.gradle
    - chmod +x ./gradlew

cache:
  key: "$CI_COMMIT_REF_NAME"
  paths:
     - .gradle/

stages:
  - build

build:
  stage: build
  script:
     - ./gradlew assembleDebug
  artifacts:
    paths:
      - app/build/outputs/apk/
```

### Bitbucket
*bitbucket-pipeline.yml*

```yml
image: javiersantos/android-ci:latest

pipelines:
  default:
    - step:
        script:
          - export GRADLE_USER_HOME=`pwd`/.gradle
          - chmod +x ./gradlew
          - ./gradlew assembleDebug
```
