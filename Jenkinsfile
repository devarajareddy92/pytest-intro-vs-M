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
                dir("${WORKSPACE}"){
                // Run SonarQube analysis for Python
                script {
                    def scannerHome = tool name: 'scanner-name', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv('sonar') {
                        sh "${scannerHome}/bin/sonar-scanner \
                            -D sonar.projectVersion=1.0-SNAPSHOT \
                            -D sonar.qualityProfile=Devarajan \
                            -D sonar.projectBaseDir=/var/lib/jenkins/workspace/Snyk-Testing/snyk-code-container-scan/appcode \
                            -D sonar.projectKey=fight \
                            -D sonar.sourceEncoding=UTF-8 \
                            -D sonar.language=python \
                            -D sonar.host.url=http://10.101.104.22:9000"
                    }
                }
            }
            }
       }
    }
}
