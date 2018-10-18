pipeline {
    agent any
    stages {
        ////////////////////////////////////////////////////
        stage('Build') {
            agent {
                docker {
                    image 'maven:3-alpine'
                    args '-v mavendb:/root/.m2'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'                
            } 
        }
        //////////////////////////////////////////////////////
 //       stage ('Copy') {
 //           steps {
 //               sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /maventarget/IRRFWeb-1.0-SNAPSHOT.war'
 //           }
 //       }
        //////////////////////////////////////////////////////
        stage ('Deploy') {
            steps {
                sh 'docker stop tomcat || true'
                sh 'docker rm tomcat || true'
                sh 'ls /mavendb/repository'
                sh 'docker run --name tomcat -d  -p 9090:8080 -v /mavendb/repository/br/com/irrfweb/IRRFWeb/1.0-SNAPSHOT:/usr/local/tomcat/webapps/ tomcat'
            }
        }
        //////////////////////////////////////////////////////
    }
}

//var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war
