pipeline {
    agent {label 'JDK_17'}
    triggers { pollSCM ('* * * * *') }
    tools {
        jdk 'JDK_17'
        maven 'maven 3.9.4'
    }
    stages {
        stage('source code') {
            steps {
                git url: 'https://github.com/saurabhcicd/spring-petclinic.git',
                    branch: 'main'
            }
        }
        stage('static code analysis') {
            steps {
                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_CLOUD') {
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=hellospc\
                        -Dsonar.token=b733cf2f18d6cfbdef80c179e62bac7f0d5e4ac4 \
                        -Dsonar.projectKey=hellospc_my-own'
                }
            }
        }
    }
}