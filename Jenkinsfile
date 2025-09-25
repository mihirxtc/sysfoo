pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Build job for the sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Test job for the sysfoo app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'Package job for the sysfoo app'
        sh '''# Truncate the GIT_COMMIT to the first 7 characters
              GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)

              # Set the version using Maven
              mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
              mvn versions:commit'''
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.6'
  }
  post {
    success {
      echo 'The build, test, and package stages were successful.'
    }

    failure {
      echo 'One or more stages failed. Please check the logs.'
    }

    always {
      echo 'Pipline execution cycle completed.'
    }

  }
  triggers {
    pollSCM('* * * * *')
  }
}