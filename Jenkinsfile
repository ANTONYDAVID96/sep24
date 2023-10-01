pipeline {
    agent any
 triggers { pollSCM('H/05 * * * * ') }
    stages {
        stage('SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/awspandian/sep24.git'
            }
        }
	stage('BUILD') {
            steps {
                sh 'mvn clean'
		sh 'mvn install'
            }
        }
	stage('Deployment') {
            steps {
		deploy adapters: [tomcat9(credentialsId: 'web', path: '', url: 'http://localhost:8585/')], contextPath: 'demo-pipe', war: '**/*.war'
            }
        }
    }
}
