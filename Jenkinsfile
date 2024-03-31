pipeline { 

    environment { 

        registry = "techaxis/tomcat" 

        registryCredential = 'dockerhub' 

        dockerImage = '' 

    }
    agent any

    
    stages { 

        stage('Cloning our Git') { 

            steps { 

                git 'git@github.com:techaxis-devops-11/CICD-Task-Nischal.git' 

            }

        } 

        

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Push image to Dockerhub') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 

        stage('Cleaning up') { 

            steps { 

                sh "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

       stage('Run Docker container on remote hosts') {

             steps {
             sh 'docker -H ssh://ubuntu@54.90.247.48 run -d -p 8086:8080 --name=helloworld5 techaxis/tomcat:$BUILD_NUMBER'
            }
           
        }
    
    }

}
