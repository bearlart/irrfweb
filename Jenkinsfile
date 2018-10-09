pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2 -v /ice/docker:/ice/docker'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
                sh 'cp /var/jenkins_home/workspace/IRRFWeb/target/IRRFWeb-1.0-SNAPSHOT.war /ice/docker'
                //sh 'cp tlt/target/tlt.war TOMCAT_DIRECTORY/webapps/'
                //sh 'mvn -B'
                //sh 'docker run hello-world'
            }
        }
    }
}
