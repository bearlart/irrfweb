
pipeline {
    environment {
       LOGIN_VAR1 = credentials('teste')
       TEST_VAR = credentials('sh-tomcat')
       COMANDO1 = credentials('parte1')
       COMANDO2 = credentials('parte2')
    }
    agent any
    stages {
        ////////////////////////////////////////////////////
        stage('Build') {
            agent {
                docker {
                    image 'maven:latest'
                    args '-v mavendb:/mavendb/'
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package install'                
            } 
        }
        //////////////////////////////////////////////////////
        stage ('Deploy') {
            steps {
                //echo $LOGIN_VAR1
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} with ${env.LOGIN_VAR1}"
                sh 'docker stop tomcat || true'
                sh 'docker rm tomcat || true'
                //sh 'ls -la /mavendb/war'
                //sh 'docker run --name tomcat -d  -p 9090:8080 -v /mavendb/war/:/usr/local/tomcat/webapps/ tomcat'
                sh "${env.TEST_VAR}"
                
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
                sh 'cp /var/jenkins_home/workspace/IRRF@2/target/IRRFWeb-1.0-SNAPSHOT.war /mavendb/war/IRRFWeb-1.0-SNAPSHOT.war'
                sh 'docker cp /mavendb/war/IRRFWeb-1.0-SNAPSHOT.war tomcat:/usr/local/tomcat/webapps/irrf.war'
                sh 'docker cp /mavendb/war/IRRFWeb-1.0-SNAPSHOT.war /ice/docker/teste.war'
            }
        }
        //////////////////////////////////////////////////////
        stage ('Activate DB') {
            steps {
                sh 'docker start mysql2 || true'
                sh 'docker network connect nrc-net tomcat || true'
                //sh "${env.COMANDO1}"
                //sh "${env.COMANDO2}"
            }
        }
        //////////////////////////////////////////////////////
    }
}

//var/jenkins_home/workspace/teste-onde-salva@2/target/IRRFWeb-1.0-SNAPSHOT.war
