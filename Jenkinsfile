pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo("checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubtoken', url: 'https://github.com/samer07/jenkins-pipeline-demo.git']])") 
                //sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo("Run unit tests using JUnit, which will ensure code fucnctions as expected") 
               // sh 'mvn test'

                echo("Run integration tests using Selenium")
                //sh 'selenium-runner --config test/config.json'
            }
            post{
                success {
                    emailext attachLog: true, 
                        body: 'Test was successful', 
                        subject: 'Test status email', 
                        to: 'kamalac777@gmail.com'
                }
                failure {
                    emailext attachLog: true, 
                        body: 'Test was Failed', 
                        subject: 'Test status email', 
                        to: 'kamalac777@gmail.com'
                }                                
            }
        }

        stage('Code Analysis') {
            steps {
                echo("Analyze the code using SonarQube")
                //withSonarQubeEnv('SonarQube') {
                  //  sh 'mvn sonar:sonar'
                //}
            }
        }

        stage('Security Scan') {
            steps {
                echo("Perform a security scan using OWASP ZAP")
                //sh 'zap-baseline.py -t http://localhost:8080/myapp -r report.html'
            }
            post{
                success {
                    emailext attachLog: true, 
                        body: 'Scan was successful', 
                        subject: 'Scan status email', 
                        to: 'kamalac777@gmail.com'
                }
                failure {
                    emailext attachLog: true, 
                        body: 'Scan was Failed', 
                        subject: 'Scan status email', 
                        to: 'kamalac777@gmail.com'
                }                                
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo("Deploy the application to a staging server using Docker")
                //sh 'docker build -t myapp .'
                //sh 'docker run -d --name myapp-staging -p 8080:8080 myapp'
            }
            
        }

        stage('Integration Tests on Staging') {
            steps {
                echo("Run integration tests on the staging environment using Selenium")
                //sh 'selenium-runner --config test/config-staging.json'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo("Deploy the application to a production server using Docker")
                /*sh 'docker stop myapp-staging'
                sh 'docker rm myapp-staging'
                sh 'docker run -d --name myapp-production -p 80:8080 myapp'*/
            }
        }
        stage('completed') {
            steps {
                echo("Completed") 
            }  
        }
    }
}
