pipeline{
    agent any
    stages{
        stage('GitCheckOut'){
            steps{
                checkout scm
            }
        }
        stage('CodeReview'){
            tools{
                maven 'Maven 3.6.1'
            }
            steps{
                dir('mavendemo'){
                    bat 'mvn checkstyle:checkstyle'
                    build job: 'PublishCheckStyleResult'
                }
            }
        }
        stage('UnitTest'){
            tools{
                maven 'Maven 3.6.1'
            }
            steps{
                dir('mavendemo'){
                    bat 'mvn test'
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy'){
            steps{
                timeout(time: 1, unit: 'DAYS'){
                    input 'Deployment Approved?'
                }
                echo 'Deployed to Production successfully'
            }
        }
    }
}
