node {
    def app
    
    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'marciozampiron-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "echo PASS ${GIT_PASSWORD}"
                        sh "echo USER ${GIT_USERNAME}"
                        sh "git config user.email marciocastelobranco3@gmail.com"
                        sh "git config user.name marciozampiron"
                        // sh "git switch main"
                        sh "cat vote-ui-deployment.yaml"
                        sh "sed -i 's+marciozampiron/vote.*+marciozampiron/vote:${DOCKERTAG}+g' vote-ui-deployment.yaml"
                        sh "cat vote-ui-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/vote-deploy.git HEAD:main"
      }
    }
  }
}
}
