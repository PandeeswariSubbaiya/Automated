pipeline {
    agent any
    stages {
        stage('Merge Release Branch') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/PandeeswariSubbaiya/Automated.git', credentialsId: 'Jenkins_Github']]])
                
                // Merge the release branch changes
                sh '''
                    git config user.name "PandeeswariSubbaiya"
                    git config user.email "PandeeswariSubbaiya1814@gmail.com"
                    git checkout main
                    git merge --no-ff dev
                    git push origin main
                '''
                
                // Create a new pull request
                sh '''
                    curl --location --request POST 'https://api.github.com' \
                    --header 'Authorization: Bearer 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' \
                    --header 'Content-Type: application/json' \
                    --data-raw '{
                        "title": "Pull request",
                        "head": "dev",
                        "base": "main"
                    }'
                '''
            }
        }
    }
}
