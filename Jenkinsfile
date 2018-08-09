pipeline {
	agent any
	stages {
		stage('Git Clone') {
			steps {
				git ([url: "https://gitlab.com/projet_ci_sll/Projet_CI.git", branch: 'master' ])
			}
		}
		stage('checkout') {
			steps { 
				 sh "git checkout master"
			}
		}
		stage('Maven Clean') {
			steps {
				sh "mvn clean"
			}
		}
		stage('Maven test') {
			steps {
				sh "mvn test"
			}
			steps {
				sh "mvn checkstyle:checkstyle"
			}
		}
		stage('Maven build') {
			steps {
				sh "mvn package"
			}
		}
		stage('Maven deploy') {
			steps {
				sh "mvn deploy"
			}
		}
	/*	stage('remove dir') {
			steps {
				deleteDir()
			}
		} */		
	}
}
