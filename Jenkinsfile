pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven1'
    }
    environment { 

        registry = "mohitkhokhar172/sample" 

        registryCredential = 'devopslearner45' 

        dockerImage = '' 

    }
    agent none
    stages{
        stage('Checkout'){
            agent any
            steps{
                git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
            }
        }
        stage('Compile'){
            agent any
            steps{
                sh 'mvn compile'
            }
        }
        stage('CodeReview'){
            agent any
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('UnitTest'){
            agent any
            steps{
                //git 'https://github.com/devops-trainer/DevOpsClassCodes.git'
                sh 'mvn test'
            }
        }
        stage('MetricCheck'){
            agent any
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
        }
        stage('Package'){
            agent any
            steps{
                sh 'mvn package'
            }
        }
    


        stage('Cloning our Git') { 
agent any
            steps { 

                git 'https://github.com/mohitkhokhar172/DevOpsClassCodes.git' 

            }

        } 

        stage('Building our image') { 
agent any
            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 
agent any
            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }

                } 

            }

        } 

        stage('Cleaning up') { 
agent any
            steps { 

                sh "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

    }



}
