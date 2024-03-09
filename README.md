In SonarAnalysis, use the below code..
```sh
sonar.projectKey=Ramya
sonar.projectName=Ramay
sonar.projectVersion=1.0
sonar.sources=/var/lib/jenkins/workspace/$JOB_NAME/src/
sonar.binaries=target/classes/com/visualpathit/account/controller/
sonar.junit.reportsPath=target/surefire-reports
sonar.jacoco.reportPath=target/jacoco.exec
sonar.java.binaries=src/main/java/com/visualpathit/account/
```
