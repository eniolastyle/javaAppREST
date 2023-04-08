@Library('jenkins-lib')
pipeline {

    agent any

    stages {

        stage('Git Checkout') {

            steps {

                script {

                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/eniolastyle/javaAppREST.git"
                    )

                }

            }

        }

    }

}