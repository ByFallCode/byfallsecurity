pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn-3.8.7"
    }

    stages {
        stage('SCM checkout') {
            steps {
                echo '-------------------- checkout ----------------------------'
                echo '---------------- ${env.BRANCH_NAME} ----------------'
                echo '---------------- ${env.JOB_NAME} ----------------'
                echo '---------------- ${env.BUILD_ID} ----------------'
            }
        }
        stage('Build') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.skip=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
