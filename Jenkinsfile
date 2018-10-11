pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v mavendb:/root/.m2'
                }
            }
        }
    }
}
