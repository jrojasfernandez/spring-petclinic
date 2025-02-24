pipeline {
    agent any

    triggers {
        cron('H/3 * * * 4')  // Runs every 3 minutes on Thursdays
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvnw clean install'
            }
        }
        stage('Test with JaCoCo') {
            steps {
                bat 'mvnw test'
                step([$class: 'JacocoPublisher',
                      execPattern: '**/target/jacoco.exec',
                      classPattern: '**/target/classes',
                      sourcePattern: '**/src/main/java',
                      exclusionPattern: '**/target/test-classes'
                ])
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
    }
}
