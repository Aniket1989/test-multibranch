pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000 -p 5000:5000' 
        }
    }
    environment {
        CI = 'true'
    }
    stages {        

        stage('Deliver for development') {
            when {
                branch 'b1'
            }
            steps {
                sh 'hello-world.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
        stage('Deploy for uat') {
            when {
                branch 'b2'
            }
            steps {
                sh 'hello-world.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

    }
}