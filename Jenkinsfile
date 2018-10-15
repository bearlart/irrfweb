pipeline {
    agent any
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v mavendb:/root/.m2 -v maventarget:/maventarget/'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'                
            }
            //stage 
        }
        stage ('Copy') {
            steps {
                sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /ice/docker/IRRFWeb-1.0-SNAPSHOT.war'
            }
        }
    }
}

//var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war
