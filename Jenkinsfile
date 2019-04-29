properties([pipelineTriggers([githubPush()])])

node('linux') 
{
    stage('Unit Tests') 
    {
        git 'https://github.com/amargurung1991/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    stage('Build') 
    {
        sh 'ant -f build.xml -v'
    }
    stage('Deploy') 
    {
        sh 'aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://amar-seis665homework10/'
    }
    stage('Report')
    {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWSJenkinsUser', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'
        }
        
    }
    
 }
