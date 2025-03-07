def gv

pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    parameters {
        // string(name: 'VERSION', defaultValue: '', description: 'Version of the application')
        choice(name: 'VERSION', choices: ['1.1.0', '1.1.1', '2.1.0'], description: 'Environment to deploy the application')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run tests?')
    }

    stages {
       
        stage('Build jar') {
            steps {
                script {
                    echo "building the application"
                    // sh 'mvn package'
                }
            }
        }

        stage('Test the application') {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    echo 'running the tests...'
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