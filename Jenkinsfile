pipeline {
    agent any
    
    stages {
        stage('configuration') {
            steps {
                echo 'BRANCH NAME: ' + env.BRANCH_NAME
                echo sh(returnStdout: true, script: 'env')
            }
        }
        
        stage('Testing') {
            steps {
                script {
                    sh 'echo "Testing"'
                    sh "cat file.txt"
					
					
					
                }
            }
        }
        
        stage("build"){
            when {
                branch 'main'
            }
            
            steps{
                sh 'echo "Build Started              dasdasd"'
            }
        }

        stage("Deploy"){
            when {
                branch 'main'
            }
            
            steps{
                sh 'echo "Deploying App"'
								
            }
        }
    }
    
    post{
        success{
            setBuildStatus("Build succeeded", "SUCCESS");
        }

        failure {
            setBuildStatus("Build failed", "FAILURE");
        } 
    }
}

void setBuildStatus(String message, String state) {
    step([
        $class: "GitHubCommitStatusSetter",
        reposSource: [$class: "ManuallyEnteredRepositorySource", url: "https://github.com/fcastelblanco/JenkinsIntegration"],
        contextSource: [$class: "ManuallyEnteredCommitContextSource", context: "ci/jenkins/build-status"],
        errorHandlers: [[$class: "ChangingBuildStatusErrorHandler", result: "UNSTABLE"]],
        statusResultSource: [$class: "ConditionalStatusResultSource", results: [[$class: "AnyBuildResult", message: message, state: state]]]
    ]);
}