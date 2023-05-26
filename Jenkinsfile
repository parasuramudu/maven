pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'cca9b619-eb7f-4cdb-aa32-094f469ed440', path: '', url: 'http://172.31.16.182:8080')], contextPath: 'test1', war: '**/*.war' 
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                input message: 'Need approval from DM!', submitter: 'srinivas'
                
                deploy adapters: [tomcat9(credentialsId: 'cca9b619-eb7f-4cdb-aa32-094f469ed440', path: '', url: 'http://172.31.23.167:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
