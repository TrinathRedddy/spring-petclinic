pipeline{
    agent{ label 'JDK17' }
    options { 
        timeout(time: 1, unit: 'HOURS') 
        retry(2)
        }
    triggers {
        cron('0 * * * *')
    }  
    parameters {
        choice(name: 'GOAL', choices: ['complie', 'package', 'clean package'])
    } 
    stages{
        stage('Source code') {
            steps {
                git url: 'https://github.com/TrinathRedddy/spring-petclinic.git',branch: 'main'
            }
        }
        stage('Build the code') {
            steps{
                sh script: "/opt/apache-maven-3.9.2/bin/mvn ${params.GOAL}"
            }
        }
        stage('Reportig and Archiving') {
            steps{
                junit testResults: 'target/surefire-reports/*.xml'
            }
        }
    } 
    post {
        success  {
            //send the success email
            echo "Succes"
        }
        unsuccessful{
            //send the unsussessful email
            echo "Failure"
        }
    }

}
