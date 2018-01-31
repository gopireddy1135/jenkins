# CI/CD Jenkins Pipeline with Code Coverage support

In this Repo we have sample java source code which is built up using maven scripts. We also have junit unit test cases suit in repo which is executed in seperate stages. We have also included sonar code analysis to the pipeline so that we can have a automative process in which if code coverage is more than 50 % ( This can be modified) we are proceeding with deployment otherwise we are simply breaking the jenkins build. We have below stages which are working in this complete CI/CD process.

Stage Checkout Code
	This will checkout the source code so that we can have source code in our jenkins working directory.

Stage Build
	We are building source code from repo using Maven build.

Stage Unit test Execution
	using maven jacoco plugin we are executing maven juint test cases here in sample source code.

Stage Integration Test
	We can configure Integration test cases also here in this stage.

Stage Sonar Analysis
	In this stage we are scanning our source code and checking the quality of source code.

Stage Code Coverage
	This will check for the coverage value from sonar portal using rest api and if coverage is more than 50 % then proceed with further stages.

Stage Archive Artifacts
	In this Stage we are archiving the artifacts so that we can download them from job builds.

Input Message 
	This will hold the job for approval click on Yes to proceed with further stages.

Stage Production Deployment
	In the last after approval we can have a production deployment in local tomcat apache webapps folder.

So using this pipeline script we can replicate a complete CI/CD process.

Further Steps:

1) We can configure a working source code to this pipeline.
2) We can implement Multi Branch pipeline concept also using the Jenkinsfile
3) We can include Ansible or any configuration management tool for deployment stage for production.
4) We can use this pipeline for Non Java builds also.
5) We can also add more quality checks tools like fortify scan.
