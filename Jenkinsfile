pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/ishaqmdgcp/jar01.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
                
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp ishaqmd/rakesh:latest'
                //sh 'docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "DOCKER_HUB", url: "https://registry.hub.docker.com" ]) {
          sh  'docker push ishaqmd/rakesh:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8008:8080 ishaqmd/rakesh"
 
            }
        }
 //stage('Run Docker container on remote hosts') {
             
   //         steps {
     //           sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
           // }
        //}
    }
	}
