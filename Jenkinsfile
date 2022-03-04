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
                        git 'https://github.com/Yugo20/Newjava.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to download the development code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'ugok.anyanwu1@gmail.com'
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
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the code', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'ugonyanwu1@gmail.com'
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
                        deploy adapters: [tomcat9(credentialsId: 'ab990aab-5e9f-4132-b630-667b91a98e2c', path: '', url: 'http://172.31.80.105:8080')], contextPath: 'test1', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                     mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the QAServer', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'ugnyanwu1@gmail.com'
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
                        git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                        sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test script failed', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'ugnanwu1@gmail.com'
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
                      deploy adapters: [tomcat9(credentialsId: 'ab990aab-5e9f-4132-b630-667b91a98e2c', path: '', url: 'http://172.31.85.147:8080')], contextPath: 'prod1', war: '**/*.war'  
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deliver into tomcat on the prodServer', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'De.ugnanwu1@gmail.com'
                        exit(1)
                    }
                }
                
            }
       }
       
   }
}
