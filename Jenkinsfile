// 1 - The pipeline definition should be tracked, in other words, 
// it has to be stored in a Jenkinsfile

pipeline {
    agent any

    tools {
        maven 'MAVEN' 
    }

    // 2 - The pipeline should include one stage which using Jacoco 
    // generates code coverage reports
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install' 
            }
        }

        stage('Code Coverage') {
            steps {
                sh './mvnw clean package jacoco:report' 

                jacoco(
                    thresholds: [
                        [threshold: 'Instruction', minimum: 0.80],
                        [threshold: 'Branch', minimum: 0.80],
                        [threshold: 'Class', minimum: 0.80],
                        [threshold: 'Method', minimum: 0.80],
                        [threshold: 'Line', minimum: 0.80]
                    ],
                    reportDir: 'target/site/jacoco' 
                )

                publishHTML(
                    publishDir: 'target/site/jacoco', 
                    displayName: 'JaCoCo Coverage Report'
                )
            }
        }
    }

    // 3 - The pipeline should be triggered every 10 minutes on Mondays
    triggers {
        cron('H/10 * * * 1') 
    }
}