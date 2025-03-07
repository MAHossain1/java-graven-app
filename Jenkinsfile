def gv

pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
           steps {
                    script {
                        checkout scmGit(
                            branches: [[name: '*/main']], // Change if needed
                            userRemoteConfigs: [[url: 'https://github.com/MAHossain1/java-graven-app.git']]
                        )
                    }
                }
        }

        stage('Build jar') {
            steps {
                script {
                    echo "building the application"
                    // sh 'mvn package'
                }
            }
        }

        stage('Building the docker image') {
            steps {
                script {
                    echo "building the docker image"
                    // withCredentials([usernamePassword(credentialsId: 'my-dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    //     sh 'docker build -t  arman04/java-maven-app:jma-3.0 .'
                    //     sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    //     sh 'docker push arman04/java-maven-app:jma-3.0'
                    // }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'deploying the application...'
                    
                }
            }    
        }

        // stage('Deploy') {
        //     steps {
        //         script {
        //             def dockerCmd = 'sudo docker run -p 3080:3080 arman04/java-maven-app:jma-2.0'
        //             sshagent(['ec2-server-key']) {
        //                 sh "ssh -o StrictHostKeyChecking=no ec2-user@35.154.210.161 ${dockerCmd}"
        //             }
        //         }
        //     }
        
        // }
    }

}