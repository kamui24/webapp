pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh ''' 
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage ('Git Secrets check') {
            steps {
                sh 'rm trufflehog || true'
                sh 'docker run trufflesecurity/trufflehog:3.88.4 git https://github.com/kamui24/webapp.git -j > trufflehog'
                sh 'cat trufflehog'
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage ('Deploy to Tomcat Webserver') {
            steps {
                sshagent(['tomcat']) {
                    sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.61.152.63:/prod/apache-tomcat/webapps/webapps.war'
                }
            }
        }
    }
}