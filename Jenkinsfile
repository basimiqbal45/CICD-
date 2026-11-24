pipeline {
    agent any
    stages {
        stage('Checkout')    { steps { checkout scm } }
        stage('Environment') { steps { sh 'java -version && javac -version' } }
        stage('Compile')     { steps { sh 'javac MatrixMultiplication.java' } }
        stage('Execute')     { steps { sh 'java MatrixMultiplication' } }
    }
    post {
        success { echo 'BUILD SUCCESSFUL' }
        failure { echo 'BUILD FAILED' }
        always  { sh 'rm -f *.class' }
    }
}
