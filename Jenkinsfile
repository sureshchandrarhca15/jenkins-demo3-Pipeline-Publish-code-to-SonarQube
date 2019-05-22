def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),
])

{
  node(label) {
     def myRepo, gitCommit, gitBranch, shortGitCommit, previousGitCommit
     stage('Checkout') 
     {
        try {
           myRepo = checkout scm
           gitCommit = myRepo.GIT_COMMIT
           gitBranch = myRepo.GIT_BRANCH
           shortGitCommit = "${gitCommit[0..10]}"
           previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)
        }
        catch(Exception e) {
           println "ERROR => Code Checkout failed, exiting..."
           throw e
        }
     }
     stage('Build') {
      try {
        container('maven') {
            sh """
              pwd
              echo "GIT_BRANCH=${gitBranch}"
              echo "GIT_COMMIT=${gitCommit}"
              id 
              mvn clean install -Dmaven.test.skip=true
            """
        }
      }
      catch (Exception e) {
        println "Failed to Maven Build - ${currentBuild.fullDisplayName}"
        throw e
      }
    }
    stage('Unit Test') {
      try {
        container('maven') {
            sh """
              pwd
              echo "GIT_BRANCH=${gitBranch}"
              echo "GIT_COMMIT=${gitCommit}"
              id 
              mvn clean test -Dmaven.test.skip=false
            """
        }
      }
      catch (Exception e) {
        println "Failed to test - ${currentBuild.fullDisplayName}"
        throw e
      }
    }
    stage('Sonar Analysis') {
      try {
        container('maven') {
            withSonarQubeEnv {
              sh "mvn -DBranch=${gitBranch} -Dsonar.branch=${gitBranch} -e -B clean sonar:sonar"
            }
        }
      }
      catch (Exception e) {
        println "Failed to Sonar - ${currentBuild.fullDisplayName}"
        throw e
      }
    }
  }
}
