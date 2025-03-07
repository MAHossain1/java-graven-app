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

        stage('init') {
            steps {
                script {
                    gv = load 'script.groovy'
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
                    gv.testApp()
                }
            }
        }
       
        stage('Build jar') {
            steps {
                script {
                    gv.buildJar()
                    // echo "building the application"
                    // sh 'mvn package'
                }
            }
        }

      

        stage('Building the docker image') {
            steps {
                script {
                    gv.buildJar()
                    // echo "building the docker image"
                    // withCredentials([usernamePassword(credentialsId: 'my-dockerhub-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    //     sh 'docker build -t  arman04/java-maven-app:jma-3.0 .'
                    //     sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    //     sh 'docker push arman04/java-maven-app:jma-3.0'
                    // }
                }
            }
        }

      

        stage('Deploy') {
            // input {
            //     message "Do you want to deploy the application?"
            //     ok "Yes"
            //     parameters {
            //         choice(name: 'ONE', choices: ['dev', 'staging', 'prod'], description: 'Environment to deploy the application')
            //          choice(name: 'TWO', choices: ['dev', 'staging', 'prod'], description: 'Environment to deploy the application')
            //     }
            // }    


            steps {
                script {
                    env.ENV = input message: 'select the environment to deploy the application', parameters: [choice(name: 'ENV', choices: ['dev', 'staging', 'prod'], description: 'Environment to deploy the application')]
                    gv.deployApp()
                    // echo "Deploying the version ${params.VERSION}"
                    // def dockerCmd = 'sudo docker run -p 3080:3080 arman04/java-maven-app:jma-2.0'
                    // sshagent(['ec2-server-key']) {
                    //     sh "ssh -o StrictHostKeyChecking=no ec2-user@35.154.210.161 ${dockerCmd}"
                    // }
                    echo "deploying to ${ENV}"
                    //  echo "deploying to ${TWO}"
                }
            }
        
        }
    }

}