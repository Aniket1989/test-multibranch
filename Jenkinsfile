pipeline {
    
    agent {
    node {
        label 'docker'        
    }
}

    stages {        

        stage('Deliver for development') {
            when {
                branch 'b1'
            }
            steps {
                sh './hello-world.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }
        stage('Deploy for uat') {
            when {
                branch 'b2'
            }
            steps {
                sh './hello-world.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

    }
}