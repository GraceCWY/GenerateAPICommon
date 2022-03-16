pipeline {
    agent any
    
    tools {nodejs "nodejs"}

    environment {
        CI = 'true'
    } 
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'npm install'
                sh 'npm run codegen -- -i petstore1.json'                                
                withCredentials([usernamePassword(credentialsId: 'git-pass-credentials-ID', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh("git tag -d some_tag")
                    sh("git tag -a some_tag -m 'Jenkins'")
//                     sh("git merge origin/release_helen")
                    sh("git clean  -d  -f .")
                     sh("git merge origin/release_helen")
                     sh("git add -A")
                    sh("git commit -m 'Merged release branch to dev'")
                     sh("git push origin/dev_helen")

                    
//                     sh("git push https://${GIT_USERNAME}:${GIT_PASSWORD}@dev_helen")

//                     sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@release') 
//                     sh('git push https://${GIT_USERNAME}:${GIT_PASSWORD}@release HEAD:release-1')                  
                }
                echo 'End Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
