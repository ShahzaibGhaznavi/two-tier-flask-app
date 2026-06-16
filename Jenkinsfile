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

        stage("Trivy Scan (Optimized)") {
            steps {
                sh '''
                    echo "Running lightweight Trivy scan..."
                    trivy fs --severity HIGH,CRITICAL --no-progress . -o results.json || true
                '''
            }
        }

        stage("Build (Fast)") {
            steps {
                sh '''
                    docker build --cache-from two-tier-flask-app \
                    -t two-tier-flask-app .
                '''
            }
        }

        stage("Test") {
            steps {
                echo "Developer test stage"
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

      stage("Deploy (FAST)") {
    steps {
        sh '''
            docker compose down
            docker compose up -d --build
        '''
    }
}
    }

    post {
        always {
            echo "Pipeline finished"
        }
    }
}
