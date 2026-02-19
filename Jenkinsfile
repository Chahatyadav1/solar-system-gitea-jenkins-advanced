pipeline{
    agent any
    tools{
         nodejs 'nodejs-22-6-0'
    }
    stages{
        stage("build"){
            steps{
            sh ''' node -v 
                   npm -v '''
            }
        }
    }
}
