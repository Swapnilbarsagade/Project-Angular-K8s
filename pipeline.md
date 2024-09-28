```groovypipeline {
    agent any
    environment {
        KUBECONFIG = credentials('kubeconfig-file')  // Jenkins credential ID for kubeconfig
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout source code from Git repository
                git url: 'https://github.com/your-repo.git', branch: 'main'
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    // Build frontend Docker image
                    sh 'docker build -t your-frontend-image:latest ./frontend'
                    // Build backend Docker image
                    sh 'docker build -t your-backend-image:latest ./backend'
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    // Push the frontend image to Docker registry
                    sh 'docker push your-frontend-image:latest'
                    // Push the backend image to Docker registry
                    sh 'docker push your-backend-image:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Deploy backend
                    sh 'kubectl apply -f backend-deployment.yaml'
                    sh 'kubectl apply -f backend-service.yaml'
                    
                    // Deploy frontend
                    sh 'kubectl apply -f frontend-deployment.yaml'
                    sh 'kubectl apply -f frontend-service.yaml'
                }
            }
        }
        stage('Post-Deployment Configuration') {
            steps {
                script {
                    // Replace worker service in the frontend pod
                    sh 'kubectl cp worker.service.ts frontend-pod:/opt/angular-frontend/src/app/services/worker.service.ts'

                    // Replace application properties in the backend pod
                    sh 'kubectl cp application.properties backend-pod:/opt/spring-backend/src/main/resources/application.properties'
                }
            }
        }
        stage('Scaling') {
            steps {
                script {
                    // Scale frontend or backend as needed
                    sh 'kubectl scale deployment frontend-app --replicas=3'
                }
            }
        }
    }
}
```

