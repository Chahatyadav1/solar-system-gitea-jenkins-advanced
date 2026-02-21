pipeline {
    agent any

    tools {
        nodejs 'nodejs-22-6-0'
    }
   environment {
        MONGO_URI = "mongodb+srv://supercluster.d83jj.mongodb.net/superData"
        MONGO_DB_CREDS = credentials('mongo-db-credentials')
        MONGO_USERNAME = credentials('mongo-db-username')
        MONGO_PASSWORD = credentials('mongo-db-password')
   }
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
                        sh 'echo "OSWAP step skip"'
                      /*
                      dependencyCheck additionalArguments: '''
                        --scan .
                       --out reports
                       --format ALL
                       --prettyPrint
                       --noupdate
                      ''',
                      odcInstallation: 'OWASP-depcheck-10'
                      */
                    }
                }

            }
        }

    }
}
