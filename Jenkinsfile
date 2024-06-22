pipeline {
    agent any
    environment {
        DJANGO_SETTINGS_MODULE = 'todo.settings'
        DOCKER_IMAGE = 'todo'
        REGISTRY_CREDENTIALS = credentials('rutujamane')
        registry = "rutujamane/to-do-app"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build registry + ":${env.BUILD_ID}"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'rutujamane') {
                        docker.image(registry + ":${env.BUILD_ID}").push('latest')
                    }
                }
            }
        }
    }
}
