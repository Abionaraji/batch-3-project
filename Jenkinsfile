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
                 withSonarQubeEnv(credentialsId: 'sonar-token', installationName: 'SonarQube') {
                     sh "mvn sonar:sonar \
                      -Dsonar.projectKey=new-project \
                      -Dsonar.host.url=http://44.203.190.217:9000 \
                      -Dsonar.login=81ce30ddc4c1381603fd993266012cada846bf0e"
                }
            }
        }
    }
}
