pipeline
{
    agent any
    stages
    {
        stage('download')
        {
            steps
            {
                
            git 'https://github.com/marutisureshk-glitch/maven1.git'
        }
        }
        stage('build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('deployment')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.21.87:/var/lib/tomcat10/webapps/test.war'
            }
        }
        stage('testing')
        {
            steps
            {
                git 'https://github.com/marutisureshk-glitch/functiontest.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('prod')
        {
            steps
            {
                sh 'scp /var/lib/jenkins/workspace/DeclarativePipeline/webapp/target/webapp.war ubuntu@172.31.29.209:/var/lib/tomcat10/webapps/prod.war'
            }
        }
    }
        post
        {
            success
            {
                echo " CICD download,build,deploy,test,prod is success"
            }
            failure
            {
                echo " CICD not build"
            }
        }
}
