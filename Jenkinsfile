pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/mavenproject.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'git failed to download te first code', cc: '', from: '', replyTo: '', subject: 'git failed', to: 'gt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build artifact', cc: '', from: '', replyTo: '', subject: 'mvn failed', to: 'dvt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.91.123:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'deploy to container failed into qa tomcat server', cc: '', from: '', replyTo: '', subject: 'dc failed', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/testingscript1.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DeclarativePE/testing.jar'
                    }
                    catch (Exception e4)
                    {
                        mail bcc: '', body: 'selenium test script failed to test artifact', cc: '', from: '', replyTo: '', subject: 'selenium failed', to: 'st@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch (Exception e5)
                    {
                        mail bcc: '', body: 'artifact failed to deliver into prodserver tomcat', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'dt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

