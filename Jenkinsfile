pipeline {
    agent any

    environment {
        TOMCAT_SERVER = "ubuntu@54.205.101.34"
        WAR_FILE = "TrainBook-1.0.0-SNAPSHOT.war"
        TOMCAT_WEBAPPS = "/home/ubuntu/tomcat/tomcat1/webapps/"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Dvinay29/demo-cicd.git'
            }
        }

        stage('Build WAR File') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    sh """
                        scp -i ~/.ssh/id_rsa target/${WAR_FILE} ${TOMCAT_SERVER}:${TOMCAT_WEBAPPS}
                        ssh -i ~/.ssh/id_rsa ${TOMCAT_SERVER} 'bash -c "cd /home/ubuntu/tomcat/tomcat1/bin && ./shutdown.sh && ./startup.sh"'
                    """
                }
            }
        }
    }
} 
