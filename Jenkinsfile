pipeline {
    agent any

    tools {
        nodejs 'nodejs-22-6-0'
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
                    }
                }

                stage("OWASP Scan") {
                    steps {
                       dependencyCheck additionalArguments: '''
                          --scan \'./\' 
                          --out \'./\' 
                          --format \'ALL\'
                          --noupdate  # i dont have api key. this check only inside machine not NVD (national vernuability database)
                          --prettyPrint''', odcInstallation: 'OWASP-depcheck-10'
                    }
                }

            }
        }

    }
}
