def secret = 'global'
def server = 'alvin@34.142.183.241'
def directory = '/home/alvin/test'
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
                  echo "deployment telah selesai"
                  exit
                  EOF"""
                }             
            }
        }
    }
}
