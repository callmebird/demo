// if docker stop myapp
// then
// echo 'stop myapp'
// docker rm myapp
// else
// echo 'myapp not run'
// fi
// docker build -t myapp .
// docker run -d -p 9090:80 --name myapp myapp

// // ## demo
// if docker stop myapp
// then
// echo 'stop myapp'
// docker rm myapp
// else
// echo 'myapp not run'
// fi
// docker build -t myapp .
// docker run -d -p 9090:80 --name myapp --net test_default --link myapi:myapi myapp

// // ## demoapi
// if docker stop myapi
// then
// echo 'stop myapi'
// docker rm myapi
// else
// echo 'myapi not run'
// fi
// docker build -t myapi .
// docker run -d --name myapi -p 3000:3000 --net=test_default --link mongodb:mongodb myapi

pipeline {
    agent none
    environment {
        imageName = 'callmebird/demo'
        port = 80
    }
    
    stages {
       stage('Package') { 
          agent {label 'mgr1'}
          steps {
              sh "docker --version"
              sh "docker build -t ${imageName} ."
            withCredentials(
                [usernamePassword(credentialsId: 'docker_hub', 
                passwordVariable: 'dockerHubPassword', 
                usernameVariable: 'dockerHubUser')]) {
              sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
              sh "docker push ${imageName}"
            }
          }
       }

       stage('Deploy') { 
          agent {label 'mgr1'}
          steps {
           sh "echo h"
          }
       }
    }
}