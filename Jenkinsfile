pipeline {
    
    agent none
    
    stages {
        stage('Checkout') {
            agent {label 'slave'}
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/makarand155/123java.git']]])
            }
        }
        
        stage('build') {
            agent {label 'slave'}
            steps {
                sh 'mvn clean package'
            }
        }
        
         stage('deploytotomcatserver') {
            agent {label 'slave'}
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcatuser', path: '', url: 'http://52.90.194.212:8080/')], contextPath: null, war: '**/*.war' 
            }
        }
    }    
}
