pipeline{

        agent {
                label "Pipeline-slave"
                }
                stages{
                        stage ("Pull the code latest from SCM"){
                                steps {
                                        git branch: 'main', url: 'https://github.com/gouravaas/new_java_docker_app.git'
                                        }
                                }
                        stage (" Build the code "){
                                steps {
					sh 'sudo mvn dependency:purge-local-repository'
                                        sh 'sudo mvn clean package'
                                        }
                                }
			stage (" Build a docker Image " ){
			     	steps {
					sh 'sudo docker build -t java-app:$BUILD_TAG .'
					sh 'sudo docker tag java-app:$BUILD_TAG Gouravaas/java-app:$BUILD_TAG'
				}
			}
                }
        }


