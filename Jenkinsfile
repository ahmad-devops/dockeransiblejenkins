pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }
    environment {
      DOCKER_TAG = getVersion()
    }
    stages {
        stage('Git Checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'freshstart', url: 'https://github.com/ahmad-devops/dockeransiblejenkins.git'
            }
        }
        stage('Maven Build') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

            }
        }
        stage('build docker image') {
            steps {
                // Get some code from a GitHub repository
                ansiblePlaybook disableHostKeyChecking: true, extras: "-e PATH=${WORKSPACE}", installation: 'ansible', inventory: 'dev.ini', playbook: 'build-docker-image.yaml'
            }
        }
    }
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}