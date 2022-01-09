pipeline {
	agent none
	stages {
	    
       stage('checkout') {
	       agent { label 'slave' }
            steps {
                sh 'sudo rm -rf hello-world-war'
	sh 'git clone https://github.com/pavithrasbidare/hello-world-war.git'	
              }
        }
	 stage('build') {
		 agent { label 'slave' }
	
            steps {
                dir('hello-world-war'){
                  sh 'pwd'
                sh 'ls'
            
                sh 'docker build -t tomcat:${BUILD_NUMBER} .'  
			
                }
	    }
	 }
                stage('push') {
			agent { label 'slave' }
	
            steps {
		    sh 'ls'
            sh 'docker tag tomcat:${BUILD_NUMBER} pavithrasbidare/pavithra:${BUILD_NUMBER}'
		    sh 'docker images'
                sh 'docker push pavithrasbidare/pavithra:${BUILD_NUMBER}'
         }
	 }
		 stage('deploy'){
		 agent { label 'slave-2' }
	     steps{
	        sh 'docker rm -f mytomcat'
	         sh 'docker run -d --name mytomcat -p 7777:8080 urssharath/myrepo:${BUILD_NUMBER}'
	     }
	 }
	
    }
}
