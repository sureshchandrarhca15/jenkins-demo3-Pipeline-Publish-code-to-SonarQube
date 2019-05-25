#!groovy
@Library('GKE-DevOps@master') _
node{ 
  /***************************************
  ***** MAVEN - Key/Value parameters *****
  ****************************************/
  maven {
     POM_FILE_LOCATION      = "pom.xml"
     MAVEN_BUILD_GOALS      = "clean install -e -Dmaven.test.skip=false"
     MAVEN_TEST_GOALS       = "test -e -Dmaven.test.skip=true"
     MAVEN_SONAR_GOALS      = "sonar:sonar"
     MAVEN_DEPLOY_GOALS     = "deploy:deploy"
     SONAR_PROJECT_KEY      = "kube-maven-sonarkey"
     SONAR_SERVER_NAME      = "SonarQubeServer"
     SONAR_PROJECT          = "Maven-Pipeline"
     MAVEN_IMAGE_NAME       = "maven"
     MAVEN_IMAGE_TAG        = "3.3.9-jdk-8-alpine"
     MAVEN_CONTAINER_NAME   = "MAVEN"
     JENKINS_WORK_DIR	      = "/home/jenkins"
     K8S_CLAIM_NAME         = "jenkins-pvc"
  }
}
