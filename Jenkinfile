pipline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                scripts {
                    git branch: 'main', url: 'https://github.com/eniolastyle/javaAppREST.git'
                }
            }
        }
    }
}