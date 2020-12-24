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
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', usernameVariable: 'AWS_KEY', passwordVariable: 'AWS_SECRET')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_KEY --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage dev --region $REGION -v --profile ${ACC_PROFILE}"
                    }
                }
            }
            stage ('Deploy HML') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', usernameVariable: 'AWS_KEY', passwordVariable: 'AWS_SECRET')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_KEY --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage hml --region $REGION -v --profile ${ACC_PROFILE}"
                    }
                }
            }
            stage ('Monitor PRD') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', usernameVariable: 'AWS_KEY', passwordVariable: 'AWS_SECRET')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_KEY --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage prd --region $REGION -v --profile ${ACC_PROFILE}"
                    }
                }
            }
        }           
}
