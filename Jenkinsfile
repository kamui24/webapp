pipeline {
    agent any
    environment {
        MAVEN_HOME = tool 'Maven'  // Получаем путь к Maven
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"  // Добавляем Maven в PATH
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
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}