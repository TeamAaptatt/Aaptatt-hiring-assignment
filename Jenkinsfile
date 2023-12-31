pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                script {
                    deleteDir()
                    sh 'git clone https://github.com/Reddykiram52/kishor-naik-Aaptatt-hiring-assignment.git'
                    sh 'pwd'
                }
            }
        }

        stage('Maven Build') {
            steps {
                script {
                    dir('kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dir('kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'docker build -t tomcat:v1 .'
                    }
                }
            }
        }

        stage('Docker Run') {
            steps {
                script {
                    // credentialsId usernameand password added in docker
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        dir('kishor-naik-Aaptatt-hiring-assignment') {
                            sh 'docker-compose down'
                            sh 'docker-compose up -d'
                        }
                    }
                }
            }
        }

        stage('Clone VM') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        sh 'docker tag tomcat:v1 reddykiram52/tomcat:v1'
                        sh 'docker push reddykiram52/tomcat:v1'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
