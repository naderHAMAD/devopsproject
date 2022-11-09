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

      
  stage('Test & Jacoco Static Analysis') {
            junit 'target/surefire-reports/**/*.xml'
            jacoco()
        }
        
           stage ('Publish to Nexus') {
            nexusPublisher nexusInstanceId: 'INSTANCE_IN_JENKINS_SETTINGS', nexusRepositoryId: 'REPO_NAME', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/gift-shop-api.war']],mavenCoordinate: [artifactId: 'gift-shop-mono', groupId: 'com.online', packaging: 'war', version: '1']]]
        }

        

    }
    
    post{

            success {
                mail to: "nader.hamad@esprit.tn",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n, More info at: ${env.BUILD_URL}",
                from: "nader.hamad@esprit.tn",
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
            }

            failure{
                mail to: "nader.hamad@esprit.tn",
                subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
                from: "nader.hamad@esprit.tn",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}"
            }

            changed{
                mail to: "nader.hamad@esprit.tn",
                subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
                from: "nader.hamad@esprit.tn",
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}"
            }
        }
}