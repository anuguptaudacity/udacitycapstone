pipeline {
    agent any
    stages {
        stage('Upload to AWS') {
            steps {
                withAWS(region:'us-east-2',credentials:'udacity_capstone') {
		        sh 'echo "Hello World with AWS"'
                
                }
            }
        }
    }
}
