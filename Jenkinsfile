// pipeline {
//     agent any
//     stages {
//         stage("Clone Git Repo"){
//             steps {
//                 git branch:"main", url:"https://github.com/kelomo2502/Configuration-management-with-helm.git"
//             }
//         }
//         stage("Build Docker Image"){
//             steps {
//                 script {
//                     docker.build("kelomo2502/restaurant-app:v4", "app")
//                 }
//             }
//         }
//         stage("Run Docker Container"){
//             steps {
//                 script {
//                     docker.image("kelomo2502/restaurant-app:v4").run("-d -p 8081:80")
//                 }
//             }
            
//         }
//     }
// }

pipeline {
    agent any

    environment {
        IMAGE_NAME = "kelomo2502/restaurant-app"
        IMAGE_TAG = "v4"
        CHART_DIR = "cafe-chart"
        RELEASE_NAME = "cafe-app"
        NAMESPACE = "default"
    }

    stages {
        stage("Clone Git Repo") {
            steps {
                git branch: "main", url: "https://github.com/kelomo2502/Configuration-management-with-helm.git"
            }
        }

        stage("Build Docker Image") {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}", "app")
                }
            }
        }

        stage("Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('', 'docker-hub-credentials-id') {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }

        stage("Deploy to Minikube via Helm") {
            steps {
                script {
                    // Update image tag in Helm values.yaml dynamically if necessary (optional)

                    // Install/upgrade release
                    sh """
                        helm upgrade --install ${RELEASE_NAME} ${CHART_DIR} \
                        --namespace ${NAMESPACE} \
                        --set image.repository=${IMAGE_NAME} \
                        --set image.tag=${IMAGE_TAG}
                    """
                }
            }
        }
    }
}
