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
	

        }
}

