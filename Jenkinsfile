pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Update Git') {
            steps {
                echo 'Build Number ${DOCKERTAG}'
                withCredentials([gitUsernamePassword(credentialsId: 'helios-jenkins-new', gitToolName: 'Default')]) {
                    // some block
                    sh "git config --global user.name hheelliiooss-admin"
                    sh "git config --global user.email developerteamhelios@gmail.com"
                    
                    sh "cat deployment.yaml"
                    sh "sed -i 's+octovianus/hms-s3-front.*+octovianus/hms-s3-front:${DOCKERTAG}+g' deployment.yaml"
                    
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins job update-deployment: ${BUILD_NUMBER}'"
                    // sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
                    // https://github.com/hheelliiooss-admin/hms-s3-front-manifest.git
                    sh "git push https://github.com/hheelliiooss-admin/hms-s3-front-manifest.git HEAD:main"
                }
            }
            
        }
    }
}
