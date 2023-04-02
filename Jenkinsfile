pipeline {
    agent any
    stages {
        stage('Test') {
            when {
                anyOf {
                    branch 'production'
                    branch 'testing'
                    branch 'development'
                }
            }
            steps {
                sh 'mvn test'
            }
        }
      stage('Build') {
            when {
                
                    branch 'production'
            
            }
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy to Production') {
            environment {
                TOMCAT_URL = 'http://3.0.176.113:8080'
                TOMCAT_USER = 'tomcat'
                TOMCAT_PASSWORD = 'tomcat'
         
            }
            when {
                branch 'production'
            }
                
            steps {
               
                sh "curl --upload-file /var/lib/jenkins/workspace/adhukara_Java_Project_Production/target/sparkjava-hello-world-1.0.war ${TOMCAT_URL}/manager/deploy?path=sparkjava-hello-world-1.0 -u ${TOMCAT_USER}:${TOMCAT_PASSWORD}"
            }
        }
    }
}
