pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('SonarQubeScan') {
            steps {
		    withSonarQubeEnv('Divyanshu Arya') {
      				sh "/home/ec2-user/apache-maven-3.8.6/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-SonarQube -Dsonar.projectName='Jenkins-SonarQube'"
    				}    
		}
        }
        
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn clean package"
            }
        }
        
        stage('Deploy') {
            steps {
                sh "docker build -t tomcat-image . "
		sh " docker run -it -d -p 8085:8080 tomcat-image:latest"
            }
        }
    }
}
