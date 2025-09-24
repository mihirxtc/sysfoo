pipeline {

    agent any

    triggers {
        pollSCM('* * * * *')
    }

    tools {
        maven 'Maven 3.9.6'
    }

    stages {
        stage('build') {
            steps {
                echo "Build job for the sysfoo app"
                sh "mvn compile"
            }
        }
        stage('test') {
            steps {
                echo "Test job for the sysfoo app"
                sh "mvn clean test"
            }
        }
        stage('package') {
            steps {
                echo "Package job for the sysfoo app"
                sh "mvn package -DskipTests"
            }
        }
    }

    post {
        success {
            echo "The build, test, and package stages were successful."
        }
        failure {
            echo "One or more stages failed. Please check the logs."
        }
        always {
            echo "Pipline execution cycle completed."
        }
    }
}