pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', credentialsId: 'github-credentials-id', url: 'https://github.com/Roshanchaure/addressbook-cicd-project'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('PMD Analysis') {
            steps {
                sh 'mvn pmd:pmd'
                publishPMD pattern: '**/target/pmd.xml'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                cp target/addressbook.war /home/ubuntu/apache-tomcat-9.0.98/webapps/
                '''
            }
        }
    }
}
