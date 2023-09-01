pipeline{
    agent any
    tools{
        maven 'Maven'
        jdk 'JDK'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'ci-jenkins', url: 'https://github.com/Abionaraji/batch-3-project.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
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
    }
}