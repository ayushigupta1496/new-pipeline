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
					sh 'sudo docker build -t new-java-app:$BUILD_TAG .'
					sh 'sudo docker tag new-java-app:$BUILD_TAG gouravaas/new-java-app:$BUILD_TAG'
				}
			}
			stage (" Push to dockerhub" ){
				steps {
					withCredentials([usernamePassword(credentialsId: 'Docker_hub', passwordVariable: 'docker_hub_pass_var', usernameVariable: 'docker_hub_user_var')]) {
					sh 'sudo docker login -u ${docker_hub_user_var} -p ${docker_hub_pass_var}'
					sh 'sudo docker push gouravaas/new-java-app:$BUILD_TAG'
}
					}
	
			}
			stage (" Testing the pipeline" ){
				steps {
					sh 'sudo docker run -dit --name java-app -p 8080:8080 new-java-app:$BUILD_TAG'
				}
			}
			stage("Testing the website"){
				steps {
					sh 'curl http://54.237.67.233:8080/java-web-app'
				}
			}
			stage("Approval status") {
				steps {
					script {
						 Boolean userInput = input(id: 'Proceed1', message: 'Promote build?', parameters: [[$class: 'BooleanParameterDefinition', defaultValue: true, description: '', name: 'Please confirm you agree with this']])
                				echo 'userInput: ' + userInput
					}
				}
			}
                }
        }


