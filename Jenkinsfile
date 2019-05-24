#!groovy
@Library('Sapient-DevOps@master') _
node{ 
 maven {
   MAVEN_BUILD_GOALS   = "clean install -e -X -Dmaven.test.skip=false"
   POM_FILE_PATH       = 'pom.xml'
   MAVEN_TEST_GOALS    = "test -e -X"
   SONAR_PROJECT_KEY   = 'kube-maven-sonarkey'
   MAVEN_SONAR_GOAL    = 'sonar:sonar'
   SONAR_SERVER_NAME   = 'SonarQubeServer'
   SONAR_PROJECT       = 'SR Kube-Pipeline'
   mavenImageName      = 'maven'
   mavenImageTag       = '3.3.9-jdk-8-alpine'
   mavenContainerName  = 'maven'
   mavenWorkDir	       = '/home/jenkins'
   mavenClaimName      = "jenkins-pvc"

}
}

