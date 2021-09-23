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
	  
	  stage ('Build')  {
	      steps {
                   sh "mvn package"
                   }
         }
    
    /* stage ('SonarQube Analysis') {
        steps {
              withSonarQubeEnv('sonar') {
                 sh 'mvn -U clean install '
				      }
          }
      } */
    }
}