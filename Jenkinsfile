pipeline {
    agent any

    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Docker Build') {
            steps {
                sh "docker build . -t ramyabojjala1809/hiring:$BUILD_NUMBER"
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([string(credentialsId: 'doker-token', variable: 'hubPwd')]) {
                    sh "docker login -u ramyabojjala1809 -p $hubPwd"
                    sh "docker push ramyabojjala1809/hiring:$BUILD_NUMBER"
                }
            }
        }
        stage('Checkout K8S manifest SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/ramyareddy1809/Hiring-app-argocd.git'
            }
        } 
        stage('Update K8S manifest & push to Repo') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'githubtoken', variable: 'GIT_TOKEN')]) { 
                        sh '''
                        cat /var/lib/jenkins/workspace/$JOB_NAME/dev/deployment.yaml
                        sed -i "s/9/${BUILD_NUMBER}/g" /var/lib/jenkins/workspace/$JOB_NAME/dev/deployment.yaml
                        cat /var/lib/jenkins/workspace/$JOB_NAME/dev/deployment.yaml
                        git add .
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push https://$GIT_TOKEN@github.com/ramyareddy1809/Hiring-app-argocd.git main
                        '''                        
                    }
                }
            }   
        }
    }
} 
