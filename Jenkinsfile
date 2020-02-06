pipeline {
    
    agent {
    node {
        label 'docker'        
    }
}

    stages {        

        stage('init') {
            steps {
                script {
                    def scmVars = checkout scm
                    env.MY_GIT_PREVIOUS_SUCCESSFUL_COMMIT = scmVars.GIT_PREVIOUS_SUCCESSFUL_COMMIT
                }
            }
        }

        stage('Deliver for development - document service') {
            when {
                allOf {
                    expression {env.BRANCH_NAME == 'b1'}
                    expression {
                        matches = sh(returnStatus:true, script: "git diff --name-only $MY_GIT_PREVIOUS_SUCCESSFUL_COMMIT|egrep -q '^packages/document/'")
                        return !matches
                    }
                }
                //branch 'b1'
            }
            steps {
                sh './hello-world.sh'
                sh './packages/document/display_application.sh'
                //input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

        stage('Deliver for development - datasync service') {
            when {
                allOf {
                    expression {env.BRANCH_NAME == 'b1'}
                    expression {
                        matches = sh(returnStatus:true, script: "git diff --name-only $MY_GIT_PREVIOUS_SUCCESSFUL_COMMIT|egrep -q '^packages/datasync/'")
                        return !matches
                    }
                }
                //branch 'b1'
            }
            steps {
                sh './hello-world.sh'
                sh './packages/document/display_application.sh'
                //input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

        stage('Deliver for development - pricing service') {
            when {
                allOf {
                    expression {env.BRANCH_NAME == 'b1'}
                    expression {
                        matches = sh(returnStatus:true, script: "git diff --name-only $MY_GIT_PREVIOUS_SUCCESSFUL_COMMIT|egrep -q '^packages/pricing/'")
                        return !matches
                    }
                }
                //branch 'b1'
            }
            steps {
                sh './hello-world.sh'
                sh './packages/document/display_application.sh'
                //input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

        stage('Deliver for development - base service') {
            when {
                allOf {
                    expression {env.BRANCH_NAME == 'b1'}                    
                }
                //branch 'b1'
            }
            steps {
                sh './hello-world.sh'
                sh './packages/display_application.sh'
                //input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

        stage('Deploy for uat') {
            when {
                branch 'b2'
            }
            steps {
                sh './hello-world.sh'
                //input message: 'Finished using the web site? (Click "Proceed" to continue)'
            }
        }

    }
}