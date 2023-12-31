pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                script {
                    sh 'rm -rf *'
                    sh 'git clone https://github.com/Reddykiram52/kishor-naik-Aaptatt-hiring-assignment.git'
                }
            }
        }
        stage('Maven Build') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'mvn clean package'
                    }
                }
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    sh 'ls'
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'pwd'
                        sh 'docker build -t tomcat:v1 .'
                    }
                }
            }
        }
        stage('Docker Run') {
            steps {
                script {
                    dir('/var/lib/jenkins/workspace/aatatt/kishor-naik-Aaptatt-hiring-assignment') {
                        sh 'docker-compose up -d'
                    }
                }
            }
        }
    }
}
