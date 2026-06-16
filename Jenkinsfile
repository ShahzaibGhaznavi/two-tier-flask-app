pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {

        stage('Code') {
            steps {
                git url: 'https://github.com/ShahzaibGhaznavi/two-tier-flask-app.git', branch: 'master'
            }
        }

        stage("Trivy File System Scan") {
            steps {
                sh '''
                    if command -v trivy >/dev/null 2>&1; then
                        trivy fs . -o results.json || true
                    else
                        echo "Trivy not installed, skipping scan"
                    fi
                '''
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }

        stage("Test") {
            steps {
                echo "Developer test kr ke dega .."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-token',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker tag two-tier-flask-app $USER/two-tier-flask-app:latest
                        docker push $USER/two-tier-flask-app:latest
                    '''
                }
            }
        }

        stage("Deploy") {
            steps {
                sh '''
                    docker compose down || true
                    docker compose up -d --build
                '''
            }
        }
    }
}
