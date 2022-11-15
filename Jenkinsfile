pipeline {
    agent any

    stages {
       stage('Pull') {
			steps{
			script{
				checkout([$class: 'GitSCM' , branches: [[name: '*/master']],
					userRemoteConfigs: [[ 
					url: 'https://github.com/BenkraiemSiwar/angularappcd.git']]])
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
		sh 'docker login -u siwar3398 -p 203jft1766'
	 }
	}
         stage('docker-registry') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml "
                }
            }

        }
         stage('docker-compose') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker-compose.yml -i ansible/inventory/host.yml "
                }
            }

        }
	

        }
}

