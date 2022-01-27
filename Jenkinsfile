node {
    def app

    stage('Clone repository') {
      

        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ramisetty1/kubernetesmanifest.git']]])
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email ramisettysiva1@gmail.com"
                        sh "git config user.name siva"
                        //sh "git switch master"
                        sh "cat springboot-deployment.yml"
                        sh "sed -i 's+ramisetty32/springboot.*+ramisetty32/springboot:${DOCKERTAG}+g' springboot-deployment.yml.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:master"
      }
    }
  }
}
}