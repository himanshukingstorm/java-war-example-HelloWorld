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
            when {
                branch 'production'
            }
                
            steps {
                script {
          deploy adapters: [tomcat9(credentialsId: 'test', url: 'http://3.0.176.113:8081/')], contextPath: '', onFailure: false, war: 'target/*.war' 
               }
                
        }
    }
       post{
        success{
            mail to: "anonymous10star@gmail.com",
            subject: "Build is successfull",
            body: "success"
        }
    failure{
      mail to: "anonymous10star@gmail.com",
            subject: "Build is failed",
            body: "failed"
    }
  }
}
