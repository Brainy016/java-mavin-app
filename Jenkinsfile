pipeline {
    agent any
    tools {
        maven 'Maven'        
    }

    stages {

        stage("build jar file") {
            steps {
                script {
                    echo 'building the application...'
                    sh "mvn package"
                }
            }
        }

        stage("build image") {
            steps {
                script {
                    echo 'building the image..'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')])
                        sh 'docker build -t brainy016/jenkins-practice:jma-2.0 .'
                        sh " echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push brainy016/jenkins-practice:jma-2.0 '
                }
            }
        }

        stage("deploy") {
            steps {
                echo 'deploying the application...'
            }
        }
    }
}
