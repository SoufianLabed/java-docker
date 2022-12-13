pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git credentialsId: 'a11c9e21-3ede-4558-9bdf-e09f7da4d2be', url: 'https://github.com/SoufianLabed/java-docker'
            }
        }
        
         stage('Build the application') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Unit Test Execution') { 
            steps{
                sh 'mvn test'
            }
        }
        stage('Build the docker image') { 
            steps{
                sh "docker build -t skyzyn/jenkins_triangle:1.0.0 ."
            }
        }
    }
      post{
          failure{
              emailext body: "Ce Build $BUILD_NUMBER a échoué",
                  recipientProviders:[requestor()], subject: "build", to:"labedsoufian@gmail.com"
          }
      }
}
