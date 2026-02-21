pipeline {
    agent any

    tools {
        nodejs 'nodejs-22-6-0'
    }
    /*
   environment {
        MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
        MONGO_DB_CREDS = credentials('mongo-db-credentials')
        MONGO_USERNAME = credentials('mongo-db-username')
        MONGO_PASSWORD = credentials('mongo-db-password')
   } */
    stages {

        stage("Installing Dependency") {
            steps {
                sh '''
                node -v
                npm -v
                '''
            }
        }

        stage("Dependency Check") {
            parallel {

                stage("Audit Scan") {
                    steps {
                         sh 'npm install mongoose@latest'
                        sh 'npm install form-data@latest'
                        sh 'npm audit --audit-level=critical'
                        sh 'echo $?'
                    }
                }

                stage("OWASP Scan") {
                    steps {
                        dependencyCheck additionalArguments: '''
                            --scan \'./\' 
                            --out \'./\'  
                            --format \'ALL\' 
                            --disableYarnAudit \
                            --prettyPrint''', odcInstallation: 'OWASP-depcheck-10'

                        dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: false
                    }
                }

            }
        }
        /* stage('Unit Testing') {
            options { retry(2) }
            steps {
                sh 'echo Colon-Separated - $MONGO_DB_CREDS'
                sh 'echo Username - $MONGO_DB_CREDS_USR'
                sh 'echo Password - $MONGO_DB_CREDS_PSW'
                sh 'npm test' 
            }
        } 

    }*/
}
}
