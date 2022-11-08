import java.text.SimpleDateFormat
pipeline {
    agent any

  

    stages {

        stage('Checkout GIT') {
            steps {
                echo 'Pulling...';
             git branch: 'nader', url: 'https://github.com/naderHAMAD/devopsproject.git'
        }

         stage("Test JUnit /Mockito"){
                steps {
                            sh 'mvn test'
                }
          }

        stage('MVN CLEAN'){
            steps{
                sh  'mvn clean'
            }
        }

      

        }

        

    }
}