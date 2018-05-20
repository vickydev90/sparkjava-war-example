node ('ubu_slave') {
	stage('Poll') {
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c4abbfe5-7b64-44d6-b375-5d85c4c4ac02', url: 'https://github.com/vickydev90/sparkjava-war-example.git']]])
	}
	
	stage('formatter') {
		sh 'mvn install'
		}
	stage('Build') {
		sh 'mvn clean verify -DskipITs=true';
		}
	
	stage('Static Code Analysis') {
		sh 'mvn clean verify sonar:sonar';
		}
	stage ('Integration test') {
		sh 'mvn clean verify -Dsurefire.skip=true';
		}
	stage ('Publish to Artifactory') {
		def server = Artifactory.server 'Default Artifactory Server'
		def uploadSpec = """{
		"files": [
		{
		"pattern": "target/hello-0.0.1.war",
		"target": "sample-java-prjct/${BUILD_NUMBER}/",
			"props": "Integration-Tested=Yes;Performance-Tested=No"
		}
			]
	}"""
	server.upload(uploadSpec)
	}
		stash includes: 'target/hello-0.0.1.war,src/pt/Hello_World_Test_Plan.jmx', name: 'binary'
}

