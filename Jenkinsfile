pipeline { 
    agent { label "node-serverless-agent"  }
    options { skipDefaultCheckout() } 
        stages { 
            stage('Checkout') {
                steps {
                    sh 'printenv'
                    checkout scm
                }
            }
            stage ('Build') { 
                steps {
                    sh "npm install"
                    sh "npm run build"
                }
            }
            stage ('Test') { 
                steps {
                    sh "echo ignore"
                }
            }
            stage ('Deploy DEV') { 
                steps {
                    sh "serverless deploy --stage dev --region $REGION -v --profile ${ACC_PROFILE_DEV}"
                }
            }
            stage ('Deploy HML') { 
                steps {
                    sh "serverless deploy --stage hml --region $REGION -v --profile ${ACC_PROFILE_HML}"
                }
            }
            stage('Confirm deploy PRD') {
                steps {
                    input 'Prosseguir para PRD?'
                }
            }
            stage ('Deploy PRD') { 
                steps {
                    sh "serverless deploy --stage prd --region $REGION -v --profile ${ACC_PROFILE_PRD}"
                }
            }
        }           
}
