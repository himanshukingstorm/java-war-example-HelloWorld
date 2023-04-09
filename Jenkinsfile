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
                anyOf{
                branch 'production'
                    branch 'testing'
                    branch 'development'
                }
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
          deploy adapters: [tomcat9(credentialsId: 'test', url: 'http://54.255.136.122:8080/')], contextPath: '', onFailure: false, war: 'target/*.war' 
               }
                
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
