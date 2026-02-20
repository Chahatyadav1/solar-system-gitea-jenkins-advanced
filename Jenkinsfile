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
                        sh 'npm audit --audit-level=critical'
                    }
                }

                stage("OWASP Scan") {
                    steps {
                        dependencyCheck additionalArguments: '''
                        --scan . 
                        --out reports 
                        --format ALL 
                        --prettyPrint
                        ''',
                        odcInstallation: 'OWASP-depcheck-10'
                    }
                }

            }
        }

    }
}
