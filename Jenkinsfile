pipeline {
  agent any
  tools {
  
  maven 'M2_HOME'
   
  }
    stages {

      stage ('Checkout SCM'){
        steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/rmspavan/cicd.git']]])
        }
      }

	  stage ('Clean and Install')  {
	      steps {
                   sh "mvn clean install"
              }
         }
    	  
	  stage ('Build')  {
	      steps {
                   sh "mvn package"
              }
         }
    
    stage ('SonarQube Analysis') {
        steps {
              withSonarQubeEnv('sonar') {
                 sh 'mvn -U clean install sonar:sonar'
				      }
          }
      }
    
	  stage ('Artifact')  {
	      steps {
           rtServer (
             id: "Artifactory",
             url: 'http://192.168.1.245:8082/artifactory',
             username: 'admin',
             password: 'P@ssw0rd',
             bypassProxy: true,
             timeout: 300
                    )    
              }
      }    
    
    }
}