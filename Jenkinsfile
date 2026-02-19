pipeline{
    agent any
    tools{
         nodejs 'nodejs-22-6-0'
    }
    stages{
        stage("Istalling Dependency"){
            steps{
            sh ''' node -v 
                   npm -v '''
            }
        }
       stage("Audit Scan"){
           steps{
               sh ' npm audit --audit-level=critical ' 
        }
    }
 }
}
