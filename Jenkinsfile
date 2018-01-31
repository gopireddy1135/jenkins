node('master') {

	def MVNHOME = tool 'Maven3'
	
stage ('checkout code'){
	checkout scm
}
	
stage ('build'){
	sh "${MVNHOME}/bin/mvn clean install"
}

stage ('Unit Test Execution'){
	sh "${MVNHOME}/bin/mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
}
	
stage ('Integration Test'){
	sh ""
}

stage ('Sonar Analysis'){
	sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000/sonar'
}
	
stage('Code Coverage ') {
//This will check for the coverage value from sonar portal using rest api and if coverage is more than 50 % then proceed with further stages
    sh "curl -o coverage.json 'http://localhost:9000/sonar/api/measures/component?componentKey=com.java.example:java-example&metricKeys=coverage';sonarCoverage=`jq '.component.measures[].value' coverage.json`;if [ 1 -eq '\$(echo '\${sonarCoverage} >= 50'| bc)' ]; then echo 'Failed' ;exit 1;else echo 'Passed'; fi"
   }

stage ('Archive Artifacts'){
	archiveArtifacts artifacts: 'target/*.war'
}

input message: "QA Team Approval for Production Deployment?"

stage ('Production Deployment'){
	sh 'cp target/*.war /opt/tomcat8/webapps'
}
}
