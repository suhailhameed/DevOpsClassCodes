pipeline{
    
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent any
    stages
    {
        stage('clone a repo')
        {
            steps{
                
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        stage('compile the code')
        {
            steps{
                sh 'mvn compile'
            }
         
            }
             stage('code review')
             {
                 steps{
                    sh  'mvn pmd:pmd' 
                 }
             }
             stage('unit test')
             {
                 steps{
                    sh  'mvn test' 
                 }
                 post{
                     success{
                         junit 'target/surefire-reports/*.xml'
                     }
                 }
                 
            }
        stage('package')
        {
            steps{
                sh 'mvn package'
            }
            post{
                success{
                    jacoco()
                }
            }
            
        }
             
            }
        }
