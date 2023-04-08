@Library('jenkins-lib') _

pipeline {

    agent any

    stages {

        stage('Git Checkout') {

            steps {

                gitCheckout(
                    branch: "main",
                    url: "https://github.com/eniolastyle/javaAppREST.git"
                )

            }

        }
        stage ('Unit Test Mavin') {

            steps {
                script {
                    mvnTest()
                }
            }

        }

    }

}