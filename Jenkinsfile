@Library('jenkins-lib') _

pipeline {

    agent any

    parameters {
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/destroy')

    }

    stages {

        stage('Git Checkout') {

        when { expression { params.action == 'create' } }

            steps {

                gitCheckout(
                    branch: "main",
                    url: "https://github.com/eniolastyle/javaAppREST.git"
                )

            }

        }
        stage ('Unit Test Maven') {

        when { expression { params.action == 'create' } }

            steps {
                script {
                    mvnTest()
                }
            }

        }
        stage ('Integration Test Maven') {
            
        when { expression { params.action == 'create' } }

            steps {
                script { 
                    mvnIntegrationTest()
                }
            }
        }
        stage ('Static code analysis: Sonarqube') {

        when { expression { params.action == 'create' } }

            steps {
                script {
                    
                    def SonarqubeCredentialsId = 'sonar-api'
                    statiCodeAnalysis(SonarqubeCredentialsId)

                }
            }
            
        }
        stage ('Quality gate status: Sonarqube') {

            when {expression { params.action == 'create' } }

            steps {
                script {
                    def SonarqubeCredentialsId = 'sonar-api'
                    QualityGateStatus(SonarqubeCredentialsId)
                }
            }
        }

    }

}