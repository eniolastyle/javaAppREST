pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                script {

                    gitCheckout(
                        branch: "main"
                    )

                }
            }
        }
    }
}