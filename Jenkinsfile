pipeline
{
    agent any
    stages 
    {
        stage ('continuous download')
        {
            steps
            {
                git 'https://github.com/keshavr21/maven_test.git'
            }
        }
        stage ('continuous build')
        {
            steps
            {
                sh '"/opt/maven/bin/mvn"  clean package'
            }
        }
        stage ('continuous deploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '8fd5c34d-ef8b-4b82-824c-0b95909e4fa8', path: '', url: 'http://172.31.36.235:8080/')], contextPath: 'testing', war: '**/*.war'
            }
        }
        stage ('continuous testing')
        {
            steps
            {
                git 'https://github.com/keshavr21/test_cases.git'
                sh 'java -jar testing.jar webapp/target/webapp.war'
            }
        }
        stage ('continuous delivery')
        {
            steps
            {
                input message: 'waiting for approval', submitter: 'harish'
                deploy adapters: [tomcat9(credentialsId: '8fd5c34d-ef8b-4b82-824c-0b95909e4fa8', path: '', url: 'http://172.31.36.235:8080/')], contextPath: 'production', war: '**/*.war'
            }
        }
    }
}
