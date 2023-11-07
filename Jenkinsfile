pipeline{
    agent any
    stages{
        stage("getting code") {
            steps {
                git url: 'https://github.com/amira123bd/DevopsTP.git', branch: 'master',
                credentialsId: 'github-credentials' //jenkins-github-creds
                sh "ls -ltr"
            }
        }

       //build de l'image
         stage("creation de image"){
            steps {                
                script {
                    echo "======== executing ========"
                        sh "mvn clean package"
            
                        sh "docker build -t devopstp ."
                       }            
                        }
                    } 
     
        stage("push to docker hub") {
            steps {                
                script {
                    echo "======== executing ========"
                        
                        sh "pwd"
                        sh "ls"
                        echo "push to hub"
                        sh "docker tag devopstp amirabd1245/devopstp:devopstp"
                        sh "docker push amirabd1245/devopstp:devopstp"
         
                           }        
                        }
                    }              
                }
            post{
                success{
                    echo "======== Setting up infra executed successfully ========"
                }
                failure{
                    echo "======== Setting up infra execution failed ========"
                }
            }

    stage('Deploy to Kubernetes') {
            steps {
                script {
                    // Apply Kubernetes configuration
                    sh "kubectl apply -f /home/hassen/RT5/kuber/static/react-app-deployment.yaml"
                }
            }
        }

        stage('Expose with Minikube') {
            steps {
                script {
                    //sh "minikube --kubeconfig $KUBECONFIG_PATH service mywebsite-service"
                    sh "KUBECONFIG=/home/hassen/.kube/config minikube service mywebsite-service"
                }
            }
        }
             
        }        
   /* 
    post{
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }*/




