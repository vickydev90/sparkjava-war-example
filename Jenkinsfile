node('docker_it') {
stage('Poll') {
	checkout scm
}
stage('Build'){
	sh 'mvn clean verify -DskipITs=true';
}
stage('Static Code Analysis'){
	sh 'mvn clean verify sonar:sonar';
}
stage ('Integration test'){
	sh 'mvn clean verify -Dsurefire.skip=true';
}
