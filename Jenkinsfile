pipeline { 
    agent any 
        stages { 
            stage ('Build') { 
                steps {
                    sh "/usr/bin/npm install"
                    sh "/usr/bin/npm run build"
                }
            }
            stage ('Test') { 
                steps {
                    sh "/usr/bin/npm run test"
                }
            }
            stage ('Deploy DEV') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "/usr/local/bin/serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET"
                        sh "/usr/local/bin/serverless deploy --stage dev --region $REGION -v "
                    }
                }
            }
            stage ('Deploy HML') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "/usr/local/bin/serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET"
                        sh "/usr/local/bin/serverless deploy --stage hml --region $REGION -v "
                    }
                }
            }
            stage ('Monitor PRD') { 
                steps {
                    withCredentials([usernamePassword(credentialsId: 'aws-credentials-all', passwordVariable: 'AWS_SECRET', usernameVariable: 'AWS_KEY')]) {
                        sh "/usr/local/bin/serverless config credentials --provider $PROVIDER --key $AWS_SECRET --secret $AWS_SECRET"
                        sh "/usr/local/bin/serverless deploy --stage prd --region $REGION -v "
                    }
                }
            }
        }           
}