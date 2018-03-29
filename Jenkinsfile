node('ubu_slave') {
	stage('Poll') {
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c4abbfe5-7b64-44d6-b375-5d85c4c4ac02', url: 'https://github.com/vickydev90/sparkjava-war-example.git']]])
	}
	stage('Build') {
	docker.image('integr-agnt').inside {
		sh 'mvn clean verify -DskipITs=true';
		}
	
		stage('Static Code Analysis') {
	sh 'mvn clean verify sonar:sonar';
		}
		stage ('Integration test') {
	sh 'mvn clean verify -Dsurefire.skip=true';
		}
	}	
}
