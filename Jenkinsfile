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
                sh 'mvn clean package jacoco:report'
                jacoco threshold: [instruction: 0.80, branch: 0.80, class: 0.80, method: 0.80, line: 0.80]
                publishHTML(targetDir: 'target/site/jacoco', reportName: 'JaCoCo Coverage Report')
            }
        }
    }

    // 3 - The pipeline should be triggered every 10 minutes on Mondays
    triggers {
        cron('H/10 * * * 1') 
    }
}