# familycashcard-spring-application-advisor-demo

Sample Spring Boot project to demonstrate Spring Application Advisor continuous upgrade capabilities.

If you want to play with this sample application and
do a manual upgrade, follow along this [Spring Academy Course - Spring Boot 2.7 to 3.1 Upgrade](https://spring.academy/courses/spring-boot-2-7-to-3-1-upgrade).

## Spring Application Advisor

See [Spring Application Advisor Documentation](https://docs.vmware.com/en/Tanzu-Spring-Runtime/Commercial/Tanzu-Spring-Runtime/index-app-advisor.html) for details.

## Install Spring Application Advisor Server

* See [Spring Application Advisor Documentation](https://docs.vmware.com/en/Tanzu-Spring-Runtime/Commercial/Tanzu-Spring-Runtime/app-advisor-install-app-advisor.html) for details.

* Make sure you have required JSON database files, e.g.

```
/tmp/spring-support-database/init-spring-projects.json
/tmp/cve-database/maven/all-cves-by-path.ndjson
```

* Get the Spring Application Advisor binaries from the private Spring repository, e.g. `application-advisor-server.jar`

* Run the Spring Application Advisor (upgrade server), e.g.

```
java -jar application-advisor-server.jar
```

* The upgrade server will run by default on http://localhost:8080 

* Let's configure the environment variable for it, e.g.

```
export APP_ADVISOR_SERVER=http://localhost:8080
```

## Get Started

* [Fork this project first](https://github.com/nevenc/familycashcard-spring-application-advisor-demo/fork), e.g.

```
git clone git@github.com:YOUR_NAME_HERE/familycashcard-spring-application-advisor-demo.git
```

* Open the project, e.g. 

```
cd familycashcard-spring-application-advisor-demo
```


## Run the Advisor CLI

* Run the Advisor to get a build configuration, e.g.

```
advisor build-config get
```

* Publish the build configuration, e.g.

```
advisor build-config publish --url=${APP_ADVISOR_SERVER}
```

* Get the Upgrade Plan, e.g. 

```
advisor upgrade-plan get --url=${APP_ADVISOR_SERVER}
```

* Apply the Upgrade Plan step, e.g.

```
advisor upgrade-plan apply --url=${APP_ADVISOR_SERVER}
```

* Alternatively, do a pull request as well. Make sure you have configured Github token (classic) for automated pull requests, e.g.

```
export GIT_TOKEN_FOR_PRS=<YOUR_GIT_TOKEN_FOR_PULL_REQUESTS>
advisor upgrade-plan apply --url=${APP_ADVISOR_SERVER} --push
```

## Rinse and repeat

* Review, and test the pull requests.

* Merge once you are comfortable with the changes.

* Rinse and repeat until you are at the latest available release, e.g. 

```
git restore .
git pull
advisor build-config get
advisor build-config publish --url=${APP_ADVISOR_SERVER}
advisor upgrade-plan get --url=${APP_ADVISOR_SERVER}
advisor upgrade-plan apply --url=${APP_ADVISOR_SERVER} --push
```
