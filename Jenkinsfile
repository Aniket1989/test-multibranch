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
                    //def scmVars = checkout scm
                    //env.MY_GIT_PREVIOUS_SUCCESSFUL_COMMIT = scmVars.GIT_PREVIOUS_SUCCESSFUL_COMMIT
                    checkout scm
                    def lastSuccessfulCommit = getLastSuccessfulCommit()
                    def currentCommit = commitHashForBuild( currentBuild.rawBuild )
                    if (lastSuccessfulCommit) {
                        commits = sh(
                        script: "git rev-list $currentCommit \"^$lastSuccessfulCommit\"",
                        returnStdout: true
                        ).split('\n')
                        println "Commits are: $commits"
                    }
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

        def getLastSuccessfulCommit() {
        def lastSuccessfulHash = null
        def lastSuccessfulBuild = currentBuild.rawBuild.getPreviousSuccessfulBuild()
        if ( lastSuccessfulBuild ) {
            lastSuccessfulHash = commitHashForBuild( lastSuccessfulBuild )
        }
        return lastSuccessfulHash
        }

        /**
        * Gets the commit hash from a Jenkins build object, if any
        */
        @NonCPS
        def commitHashForBuild( build ) {
        def scmAction = build?.actions.find { action -> action instanceof jenkins.scm.api.SCMRevisionAction }
        return scmAction?.revision?.hash
        }

    }
}