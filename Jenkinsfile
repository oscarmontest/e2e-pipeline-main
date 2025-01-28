pipeline{
    agent{
        label "JenkinsAgent"
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    
    environment {
        APP_NAME = "e2e-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER = "oscarmontes"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
        JENKINS_API_TOKEN = credentials("1114d87a17acdda05b959f4a46b90fa612")
    }
    

    stages{

      stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
    
        stage("Checkout from SCM"){
            steps {
                git branch: 'main', credentialsId: 'oscarmontest', url: 'https://github.com/oscarmontest/e2e-pipeline-main.git'
            }

        }
    
            stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

        }

        stage("Test Application"){
            steps {
                sh "mvn test"
            }

        }
    }
}
