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
        stage ('SONAR ANALYSIS') {
            steps {
                 withSonarQubeEnv(credentialsId: 'sonar-jenkins', installationName: 'SonarQube') {
                     sh '''sonar.projectKey=my.only.project
                         sonar.projectName=My Nice Project
                         sonar.projectVersion=main
                         sonar.sources=Vendor2/Project/src/
                         sonar.java.binaries=Vendor2/Project/src/
                         sonar.java.source=1.8'''
                }
            }
        }
    }
}
