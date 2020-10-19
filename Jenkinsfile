pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven1'
    }
    environment { 

        registry = "devopslearner45/myrepo" 

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
                bat 'mvn package'
            }
        }
    


        stage('Cloning our Git') { 

            steps { 

                git 'https://github.com/madhuri-stack/DevOpsClassCodes/edit/master/JenkinsFile1' 

            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 

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

    }



}
