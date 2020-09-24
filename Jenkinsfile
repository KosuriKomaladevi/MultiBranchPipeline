  
@Library('shared-library-github')_
pipeline {
    agent any
     options {
        skipDefaultCheckout true
    }
    tools {
        maven 'Maven3' 
    }
    
    stages{
        stage('checkout SCM'){
            steps{
                script{
                    toCheckout([
                        branch:'master',
                        url:'https://github.com/KosuriKomaladevi/MultiBranchPipeline.git'
                    ])
                }
            }
        }
         stage('build stage'){
            steps{
                script{
                    toBuild()
                }
            }
        }
        stage('package stage'){
            steps{
                script{              
                    toPackage()
                }
            }
        }

        
     
       stage('Deploying to Artifactory'){
             steps{
                 script{
                    artifactory([
                        server : 'artifactory',
                        tool :"Maven3" 
                    ])
                 }
             }
         }
        stage('Deploying to Tomcat Server'){
            steps{
                script{
                    deployToTomcat([
                               adapters: [tomcat8(credentialsId: 'tomcat-manager-credentials', path: '', url: 'http://localhost:9090')], 
                               contextPath: 'MyApplication',
                               war: '" **/*.war"'
                    ])
                    
                    
                }
            }
        }
        
        }
    }
