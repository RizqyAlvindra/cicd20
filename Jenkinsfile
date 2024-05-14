def secret = 'global'
def server = 'aimingds@103.127.97.23'
def directory = '/home/aimingds/dumbplay-frontend'
def branch  = 'master'
def namebuild = 'lolrandom'
def tag = 'staging'

pipeline {
    agent any
    stages{
	stage ('pull new code') {
	   steps{
		sshagent([secret]){
		   sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
		   cd ${directory}
		   git pull origin ${branch}
		   echo "Pulling new code telah selesai"
                   exit
                   EOF"""
	       }
	    }
         }
          
        stage ('build the code') {
           steps{
               sshagent([secret]){
                  sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                  cd ${directory}
                  docker buildx build -t ${namebuild}:${tag} .
                  echo "Build code telah selesai"
                  exit
		  EOF""" 
  	        }	
             }
          } 

        stage ('deploy') {
           steps {
               sshagent([secret]){
                  sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                  cd ${directory}
                  docker compose down
                  docker compose up -d
                  echo "deployment telah selesai"
                  exit
                  EOF"""
                }             
            }
        }
    }
}
