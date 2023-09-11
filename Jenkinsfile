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
                                        sh 'sudo mvn clean package'
                                        }
                                }
                }
        }
}

