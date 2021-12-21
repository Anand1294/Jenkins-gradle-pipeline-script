def url = env.RUN_DISPLAY_URL

url = url.replace("display/redirect","console")

pipeline {
    agent any

        tools
        {
        jdk 'JAVA_HOME'
        }
        stages {
        stage('Checkout') {
            steps {
                cleanWs()
                git branch: 'main', url: 'https://github.com/Anand1294/Spring-demo.git'
            }
        }
        stage('Build') {
            steps {
                bat 'gradlew.bat clean build'
            }
        }
    }
    post {
        always {
            junit 'build/test-results/**/*.xml'
        }
        success {
            mail body: "This is Jenkins Mail.\n${env.JOB_NAME} run successful.\nPlease verify the build result using the mentioned link : ${url}.\n\nThe job can also be accessed using the mentioned link : ${env.JOB_DISPLAY_URL}",
                subject: "Jenkins Success Build ${env.JOB_NAME}",
                to: "shubhamanand1203@gmail.com" 
        }
        failure {
            mail body: "This is Jenkins Mail.\n${env.JOB_NAME} execution failed.\nPlease verify and troubleshoot the build result using the mentioned link : ${url}.\n\nThe job can also be accessed using the mentioned link : ${env.JOB_DISPLAY_URL}",
                subject: "Jenkins Fail Build ${env.JOB_NAME}",
                to: "shubhamanand1203@gmail.com" 
        }
    }
}
