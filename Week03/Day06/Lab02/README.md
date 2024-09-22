## Create a Jenkins Freestyle job that pulls code from a GitHub repository(from your choise) and builds it using Maven.
###    Set up the job to trigger a build whenever there is a change in the GitHub repository.
- Done
---------------------------------------------------------------------------------------
## Configure a Jenkins pipeline job that checks out code from Git, builds it, and runs unit tests.
###    Use declarative syntax for the pipeline.
```
pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven' // Reference to your Maven installation in Jenkins
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from Git
                git branch: 'main', url: 'https://github.com/username/repository.git'
            }
        }
        
        stage('Build') {
            steps {
                // Run Maven clean and install commands to build the project
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }
        
        stage('Run Unit Tests') {
            steps {
                // Run Maven test command to execute unit tests
                sh "${MAVEN_HOME}/bin/mvn test"
            }
        }
    }
    
    post {
        // Archive test results and artifacts
        always {
            junit 'target/surefire-reports/*.xml' // Adjust path based on your project structure
            archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
        }
        
        // Notify if the pipeline failed
        failure {
            mail to: 'team@example.com',
                 subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Something went wrong. Please check the Jenkins build log."
        }
    }
}
```
---------------------------------------------------------------------------------------
## Set up a Jenkins job to trigger an automatic build whenever a push is made to the main branch of a GitHub repository and make sure that there is another branches.
###   Use the Git plugin and a webhook to accomplish this.
- Done
---------------------------------------------------------------------------------------
## Create a Jenkins job that builds a Docker image and pushes it to Docker Hub.
    Use Jenkins credentials to securely store your Docker Hub credentials.
- Done
---------------------------------------------------------------------------------------
## Set up a Jenkins pipeline that sends notifications to a Slack channel upon build success or failure.
    Configure Slack integration using the appropriate plugin.
```
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Example: Checkout code from Git repository
                git branch: 'main', url: 'https://github.com/username/repo.git'
            }
        }
        
        stage('Build') {
            steps {
                // Example: Build the project using Maven
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Example: Run unit tests
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            slackSend (channel: '#build-notifications', 
                       color: 'good', 
                       message: "Build SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (<${env.BUILD_URL}|Open>)")
        }
        
        failure {
            slackSend (channel: '#build-notifications', 
                       color: 'danger', 
                       message: "Build FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (<${env.BUILD_URL}|Open>)")
        }
        
        always {
            // You can also send additional notifications here (e.g., for unstable builds)
            echo 'Build complete.'
        }
    }
}
```
---------------------------------------------------------------------------------------
## Create a Jenkins pipeline that pulls code from a Git repository, builds it, and deploys it to a Kubernetes cluster.
###    Use Kubernetes CLI commands within the pipeline to manage deployments.
```
pipeline {
    agent any
    
    environment {
        // Define environment variables for your Docker registry and Kubernetes cluster
        DOCKER_REGISTRY = 'your-registry-url'
        IMAGE_NAME = 'your-image-name'
        KUBERNETES_NAMESPACE = 'your-namespace'
        KUBE_DEPLOYMENT = 'your-deployment-name'
        DOCKER_CREDENTIALS = 'docker-credentials-id'  // Jenkins credentials ID for Docker registry
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository from Git
                git branch: 'main', url: 'https://github.com/username/repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    sh """
                        docker build -t ${DOCKER_REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER} .
                    """
                }
            }
        }

        stage('Push to Docker Registry') {
            steps {
                script {
                    // Log in to Docker registry and push the image
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS}", passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        sh """
                            echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin ${DOCKER_REGISTRY}
                            docker push ${DOCKER_REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER}
                        """
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Use kubectl to deploy the new image to Kubernetes
                    sh """
                        kubectl set image deployment/${KUBE_DEPLOYMENT} ${KUBE_DEPLOYMENT}=${DOCKER_REGISTRY}/${IMAGE_NAME}:${env.BUILD_NUMBER} --namespace=${KUBERNETES_NAMESPACE}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "Deployment succeeded!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
```
