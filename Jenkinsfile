pipeline {
    agent any

    environment {
        TABETABLE_REPO = 'https://github.com/f-lab-edu/tabetable.git'
        CREDENTIALS_ID = credentials('github-personal-access-token')
    }

    stages {
        stage('Clone tabetable Repository') {
            steps {
                dir('tabetable') {
                    git url: "${TABETABLE_REPO}", credentialsId: "${CREDENTIALS_ID}", branch: 'feature/user-service'
                }
            }
        }

        stage('Build') {
            steps {
                dir('tabetable') {
                    sh './gradlew clean build'
                }
            }
        }

        stage('Test') {
            steps {
                dir('tabetable') {
                    sh './gradlew test'
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                dir('tabetable') {
                    script {
                        def imageTag = "f-lab-edu/tabetable:latest"
                        sh "docker build -t ${imageTag} ."
                        sh "docker push ${imageTag}"
                    }
                }
            }
        }
    }
}