pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                //git credentialsId: 'f87a34a8-0e09-45e7-b9cf-6dc68feac670', 
                //url: 'https://github.com/iam-veeramalla/cicd-end-to-end',
                //branch: 'main'
               git branch: 'main', url: 'https://github.com/ShriLahe/cicd-end-to-end.git'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t 326598147/cici-repo:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    withCredentials([string(credentialsId: '326598147', variable: 'dockerhubjenkins')]) {
               }
                    sh '''
                    docker login -u pradipak4me@gmail.com -dockerhubjenkins
                    echo 'Push to Repo'
                    docker push 326598147/cici-repo:${BUILD_NUMBER}
                    '''
                }
            }
        }
        /*
        stage('Checkout K8S manifest SCM'){
            steps {
                git credentialsId: 'f87a34a8-0e09-45e7-b9cf-6dc68feac670', 
                url: 'https://github.com/iam-veeramalla/cicd-demo-manifests-repo.git',
                branch: 'main'
            }
        }
        
        stage('Update K8S manifest & push to Repo'){
            steps {
                script{
                    withCredentials([usernamePassword(credentialsId: 'f87a34a8-0e09-45e7-b9cf-6dc68feac670', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh '''
                        cat deploy.yaml
                        sed -i '' "s/32/${BUILD_NUMBER}/g" deploy.yaml
                        cat deploy.yaml
                        git add deploy.yaml
                        git commit -m 'Updated the deploy yaml | Jenkins Pipeline'
                        git remote -v
                        git push https://github.com/iam-veeramalla/cicd-demo-manifests-repo.git HEAD:main
                        '''                        
                    }
                }
            }
        }*/
    }
}
