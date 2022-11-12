pipeline {
    agent any

    stages {
       stage('Pull') {
			steps{
			script{
				checkout([$class: 'GitSCM' , branches: [[name: '*/master']],
					userRemoteConfigs: [[ 
					url: 'https://github.com/BenkraiemSiwar/CD_Projet.git']]])
				}
			}
		}
       stage('build') {
	    	       steps{
	     		   script{
	     		       
	          		sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml "
	           }
	        }
	    }
       stage('docker') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml "
                }
            }

        }
         stage('Login Dockerhub') {

	    steps {
		sh 'docker login -u siwar3398 -p 203JFT1766'
	 }
	}
         stage('docker-registry') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml "
                }
            }

        }
	

        }
}

