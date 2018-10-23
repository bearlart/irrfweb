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
                sh 'mvn -B -DskipTests clean package install'                
            } 
        }
        //////////////////////////////////////////////////////
        stage ('Copy') {
            steps {
                //sh 'mkdir /mavendb/war/ || true'
                //sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /mavendb/war/ROOT.war'
                
                sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /maventarget/IRRFWeb-1.0-SNAPSHOT.war'
            //}
        }
        //////////////////////////////////////////////////////
        stage ('Deploy') {
            steps {
                sh 'docker stop tomcat || true'
                sh 'docker rm tomcat || true'
                //sh 'ls -la /mavendb/war'
                //sh 'docker run --name tomcat -d  -p 9090:8080 -v /mavendb/war/:/usr/local/tomcat/webapps/ tomcat'
                
                sh 'docker run --name tomcat -d  -p 9090:8080 -v /maventarget/IRRFWeb-1.0-SNAPSHOT.war:/usr/local/tomcat/webapps/irrf.war tomcat'
                sh 'ls -la /maventarget/'
            }
        }
        //////////////////////////////////////////////////////
    }
}

//var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war
