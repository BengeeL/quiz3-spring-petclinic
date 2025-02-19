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

        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('JaCoCo Report') {
            steps {
                jacoco(
                    execPattern: '**/target/jacoco.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src/main/java'
                )
            }
        }
    }

    post {
        always {
            jacoco(
                execPattern: '**/target/jacoco.exec',
                classPattern: '**/target/classes',
                sourcePattern: '**/src/main/java'
            )
        }
    }

    // 3 - The pipeline should be triggered every 10 minutes on Mondays
    triggers {
        cron('H/10 * * * 1') 
    }
}