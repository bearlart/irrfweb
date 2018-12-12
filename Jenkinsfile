pipeline {
    agent any
    environment {
        LOGIN = credentials('logincreds')
    }
    stages {
        ////////////////////////////////////////////////////
        stage('Build') {
            agent {
                docker {
                    image 'maven:latest'
                    args '-v mavendb:/root/.m2'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package install'                
            } 
        }
        //////////////////////////////////////////////////////
        stage ('Deploy') {
            steps {
                echo $LOGIN
                sh 'docker stop tomcat || true'
                sh 'docker rm tomcat || true'
                //sh 'ls -la /mavendb/war'
                //sh 'docker run --name tomcat -d  -p 9090:8080 -v /mavendb/war/:/usr/local/tomcat/webapps/ tomcat'
                sh 'docker run --name tomcat -d  -p 9090:8080  tomcat'
                
                //sh 'ls -la /maventarget/'
            }
        }
        //////////////////////////////////////////////////////
        stage ('Copy') {
            steps {
                sh 'mkdir /mavendb/war/ || true'
                //sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /mavendb/war/ROOT.war'
                //sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /maventarget/IRRFWeb-1.0-SNAPSHOT.war'
                //sh 'docker cp /maventarget/IRRFWeb-1.0-SNAPSHOT.war tomcat:/usr/local/tomcat/webapps/irrf.war'
                sh 'cp /var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war /mavendb/war/IRRFWeb-1.0-SNAPSHOT.war'
                sh 'cp /mavendb/war/IRRFWeb-1.0-SNAPSHOT.war tomcat:/usr/local/tomcat/webapps/irrf.war'
            }
        }
        //////////////////////////////////////////////////////
        stage ('Activate DB') {
            steps {
                sh 'docker start mysql2 || true'
                sh 'docker network connect nrc-net tomcat || true'
            }
        }
        //////////////////////////////////////////////////////
    }
}

//var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war
