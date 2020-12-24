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
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage dev --region $REGION -v "
                    }
                }
            }
            stage ('Deploy HML') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage hml --region $REGION -v "
                    }
                }
            }
            stage ('Monitor PRD') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET --profile ${ACC_PROFILE} --overwrite"
                        sh "serverless deploy --stage prd --region $REGION -v "
                    }
                }
            }
        }           
}
