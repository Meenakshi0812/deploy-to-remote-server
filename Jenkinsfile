pipeline {
    agent any

    stages {
        stage('Clone Git Repository') {
            steps {
                script {
                    def clonePath = "/home/ubuntu/build_${env.BUILD_NUMBER}"
                    dir(clonePath) {
                        git branch: 'main', url: 'https://github.com/Meenakshi0812/https://github.com/Meenakshi0812/deploy-to-remote-server.git'
                    }
                }
            }
        }

        stage('Create Zip File') {
            steps {
                script {
                    def folderName = "build_${env.BUILD_NUMBER}"
                    def zipFileName = "${folderName}.zip"
                    sh "cd /home/ubuntu && zip -r ${zipFileName} ${folderName}/*"
                }
            }
        }

        stage('Copy Zip File to Remote Server') {
            steps {
                script {
                    def zipFileName = "build_${env.BUILD_NUMBER}.zip"
                    def destinationPath = "/var/www/html/"
                    sh "scp -o StrictHostKeyChecking=no /home/ubuntu/${zipFileName} ubuntu@35.173.124.74:${destinationPath}"
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    def folderName = "build_${env.BUILD_NUMBER}"
                    def zipFileName = "${folderName}.zip"
                    def destinationPath = "/var/www/html/"

                    sh "ssh -o StrictHostKeyChecking=no ubuntu@35.173.124.74 'unzip -o ${destinationPath}${zipFileName} -d ${destinationPath}'"
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@35.173.124.74 'ln -sfn ${destinationPath}${folderName} ${destinationPath}code'"
                }
            }
        }
    }
}
