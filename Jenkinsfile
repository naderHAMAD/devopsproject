import java.text.SimpleDateFormat
pipeline {
    agent any

  

    stages {

        stage('Checkout GIT') {
            steps {
                echo 'Pulling...';
             git branch: 'nader', url: 'https://github.com/naderHAMAD/devopsproject.git'
        }
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
         stage('MVN COMPILE'){
            steps{
                sh  'mvn compile'
            }
        }

        stage('MVN PACKAGE'){
              steps{
                  sh  'mvn package'
              }
        }
      
    
	

          stage('MVN SONARQUBE'){

                steps{
                          sh  'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
                }
          }

      
 
        

    }
    
    post {
        always {
	mail bcc: '', body: 'Ceci est un test de mailing', cc: '', from: '', replyTo: '', subject: 'Jenkins-buils-Notification', to: 'rm.nader.28@gmail.com'
 
}
}
}