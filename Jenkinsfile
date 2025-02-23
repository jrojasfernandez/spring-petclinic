pipeline {
    agent any

    triggers {
        cron('H/3 * * * 4')  // Every 3 minutes on Thursdays
    }

    stages {
        stage('Build') {
            steps {
                sh './mvnw clean install'
            }
        }
        stage('Test with JaCoCo') {
            steps {
                sh './mvnw test'
            }
            post {
                always {
                    jacoco execPattern: '**/target/jacoco.exec',
                           classPattern: '**/target/classes',
                           sourcePattern: '**/src/main/java',
                           exclusionPattern: '**/target/test-classes'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
