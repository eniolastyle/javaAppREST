@Library('jenkins-lib') _

pipeline {

    agent any

    parameters {
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/destroy')
        string(name: 'ImageName', description: 'name of the docker image', defaultValue: 'javapp')
        string(name: 'ImageTag', description: 'tag of the docker image', defaultValue: 'v1')
        string(name: 'DockerHubUser', description: 'name of the application', defaultValue: 'abooumair')

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
        // stage ('Unit Test Maven') {

        // when { expression { params.action == 'create' } }

        //     steps {
        //         script {
        //             mvnTest()
        //         }
        //     }

        // }
        // stage ('Integration Test Maven') {
            
        // when { expression { params.action == 'create' } }

        //     steps {
        //         script { 
        //             mvnIntegrationTest()
        //         }
        //     }
        // }
        // stage ('Static code analysis: Sonarqube') {

        // when { expression { params.action == 'create' } }

        //     steps {
        //         script {
                    
        //             def SonarqubeCredentialsId = 'sonar-api'
        //             statiCodeAnalysis(SonarqubeCredentialsId)

        //         }
        //     }
            
        // }
        // stage ('Quality gate status: Sonarqube') {

        //     when { expression { params.action == 'create' } }

        //     steps {
        //         script {
        //             def SonarqubeCredentialsId = 'sonar-api'
        //             QualityGateStatus(SonarqubeCredentialsId)
        //         }
        //     }
        // }
        stage ('Maven build : maven') {
            
           when { expression { params.action == 'create' } }

           steps {
                script {
                    mvnBuild()
                }
           } 
        }
        stage ('Docker image build') {
            when { expression { params.action == 'create'}}

            steps {
                script {
                    dockerBuild("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
                }
            }
        }
        stage ('Docker image scan: trivy') {
            when { expression {params.action == 'create'}}

            steps {
                script {
                    dockerImageScan("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
                }
            }
        }
        stage ('Docker image push: DockerHub') {
            when {expression {params.action == 'create'}} 

            steps {
                script {
                    dockerImagePush("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
                }
            }
        }
        stage ('Docker Image Cleanup') {
            when {expression {params.action == 'create' }}
            
            steps {
                script {
                    dockerImageCleanup("${params.ImageName}", "${params.ImageTag}", "${params.DockerHubUser}")
                }
            }
        }
    }

}