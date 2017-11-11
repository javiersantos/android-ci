<h1 align="center">Android CI <a href="https://hub.docker.com/r/javiersantos/android-ci/"><img src="https://img.shields.io/docker/automated/javiersantos/android-ci.svg"></a></h1>
<h4 align="center">Continous Integration (CI) for Android apps on GitLab / Bitbucket</h4>

<p align="center">An image for building Android apps with support for multiple SDK Build Tools. This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool. Based on <a href="https://github.com/jangrewe/gitlab-ci-android">jangrewe/gitlab-ci-android</a>.</p>

## Available images
### javiersantos/android-ci:latest
Includes the latest SDK Build Tools and SDK Platform.

* Build Tools: 26.0.2
* Platform: Android 25, 26 & 27
* Android Support: Constraint Layout 1.0.2 & Constraint Layout Solver 1.0.2

## Sample usage
### GitLab
*.gitlab-ci.yml*

```yml
image: javiersantos/gitlab-ci:latest

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
image: javiersantos/gitlab-ci:latest

pipelines:
  default:
    - step:
        script:
          - export GRADLE_USER_HOME=`pwd`/.gradle
          - chmod +x ./gradlew
          - ./gradlew assembleDebug
```