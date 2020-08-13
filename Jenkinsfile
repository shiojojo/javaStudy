pipeline {
    agent { docker 'maven:3.6.3-openjdk-15' }
    environment {
        work_dir='docoTsubu'
        // bundle='/home/jenkins/bin/bundle'
        // deploy_dir='/home/jenkins/deploy'
    }

    stages {
        stage('Build') {
            steps {

                // Get some code from a GitHub repository
                git 'https://github.com/shiojojo/javaStudy.git'
                dir(work_dir) {
                    // Run Maven on a Unix agent.
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"
                }
                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    dir(work_dir) {
                        // junit '**/target/surefire-reports/TEST-*.xml'
                        archiveArtifacts 'target/*.war'
                    }
                }
            }
        }
    }
}
