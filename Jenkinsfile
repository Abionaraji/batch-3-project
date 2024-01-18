pipeline{
    agent any
    tools{
        maven 'Maven'
        jdk 'JDK'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/Abionaraji/batch-3-project.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
            post{
                success{
                    echo 'New achiving'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Unit Test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('Integrated Testing'){
            steps{
                sh 'mvn verify -DiskipUnitTests'
            }
        }
       stage('SonarQube Analysis') {
           def mvn = tool 'Default Maven';
               withSonarQubeEnv(credentialsId: 'sonar-token', installationName: 'SonarQube') {
               sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=new-project -Dsonar.projectName='new-project'"
          }
       }
    }
}
