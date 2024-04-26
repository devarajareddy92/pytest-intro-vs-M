pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devarajareddy92/pytest-intro-vs-M.git']]])
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/devarajareddy92/pytest-intro-vs-M.git'
                sh 'python3 ops.py'
            }
        }
        stage('Test') {
            steps {
                sh 'python3 -m pytest'
            }
        }
stage('SonarQube Code Analysis') {
    steps {
        dir("${WORKSPACE}") {
            script {
                def scannerHome = tool name: 'scanner-name', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                withSonarQubeEnv('sonar') {
                    sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectVersion=1.0-SNAPSHOT \
                        -Dsonar.qualityProfile=Devarajan \
                        -Dsonar.projectBaseDir=${WORKSPACE}/snyk-code-container-scan/appcode \
                        -Dsonar.projectKey=fight \
                        -Dsonar.sourceEncoding=UTF-8 \
                        -Dsonar.language=python \
                        -Dsonar.host.url=http://10.101.104.22:9000
                    """
                }
            }
        }
    }
}

    }
}
