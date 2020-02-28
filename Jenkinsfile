pipeline {
    agent any

    stages {
        stage('test  stage') {
            steps {
                bat "mvn -Dmaven.test.failure.ignore=true test -Dsurefire.suiteXmlFiles=/src/test/resources/country.xml"
            }
        }
        stage('result stage') {
            steps {
               step([$class: 'Publisher', reportFilenamePattern: '**/testng-results.xml'])
            }

            post {
                success {
                    telegramSend "Build was successfull, link: ${BUILD_URL}"
                }
                failure {
                    telegramSend "Build was failure, link: ${BUILD_URL}"
                }
                unstable {
                    telegramSend "Build was unstable, link: ${BUILD_URL}"
                }
            }
        }
        stage('echo stage') {
            steps {
                echo "echo!"
            }
        }

    }
}