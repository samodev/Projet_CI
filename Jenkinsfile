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
		stage('parallel tests') {
				parallel(
					stage('Maven test') {
						steps {
							sh "mvn test"
						}
					},
					stage('checkstyle') {
						steps {
							sh "mvn checkstyle:checkstyle"
						}
						post {
							always {
                               					 step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', checkstyle: 'gitlist-PHP/build/logs/phpcs.xml'])
							}
						}
                                	}
				)
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
