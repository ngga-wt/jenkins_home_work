pipeline {
    agent any
    environment {
        START_TIME = sh(script: 'date +"%Y-%m-%d %H:%M:%S"',returnStdout: true).trim()
        buildUser = 'anonymous'
      }
    stages {
        stage('Start stage') {
            steps {
                // Print Environment variables and sleep 5 seconds
                echo "START_TIME: [$START_TIME] ,BUILD_NUMBER: $BUILD_NUMBER ,JOB_NAME: $JOB_NAME AND The building user name: ${buildUser}"
                sleep 5
            }
        }
        stage('Change Environment') {
            steps {
                script {

                    // Change buildUser environment variable
                    buildUser = sh(script: 'whoami', returnStdout: true).trim()

                    // Print output to console
                    echo "START_TIME: [$START_TIME] ,BUILD_NUMBER: $BUILD_NUMBER ,JOB_NAME: $JOB_NAME AND The building user name after changed is running as: ${buildUser}"
                }
            }
        }
        stage('Last stage') {
            steps {
                    script {

                    def END_TIME = sh(script: 'date +"%Y-%m-%d %H:%M:%S"', returnStdout: true)

                    // Convert dates to epoch seconds
                    def START_SECS = sh(script: "date -d \"$START_TIME\" +%s", returnStdout: true).toInteger()
                    def END_SECS = sh(script: "date -d \"$END_TIME\" +%s", returnStdout: true).toInteger()

                    // Calculate the difference
                    def DIFF_SECS = END_SECS - START_SECS 

                    // Convert seconds back to a human-readable format
                    def DIFF_HUMAN=sh(script: "date -d \"@$DIFF_SECS\" +'%H:%M:%S' -u", returnStdout: true)

                    def MINUTES = DIFF_SECS / 60
                    def SECONDS = DIFF_SECS % 60
                    
                    sh """
                        echo "BUILD_NUMBER: $BUILD_NUMBER ,JOB_NAME: $JOB_NAME AND The building user name in differnt stage is running as: ${buildUser}"
                        echo "START_TIME: [$START_TIME], END_TIME: [$END_TIME] Duration: in minutes: $MINUTES ,in seconds: $SECONDS ,HUMAN_READABLE_TIME_DIFFRENCES $DIFF_HUMAN"
                    """
                }
            }
        }
    }
}
