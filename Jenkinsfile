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
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://amar-seis665homework10/'
    }
   
}
