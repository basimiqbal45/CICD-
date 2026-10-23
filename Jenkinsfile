node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/basimiqbal45/CICD-'
        )
    }

    stage('Deploy to EC2'){
        echo 'Deploying to EC2'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R \$(whoami):\$(whoami) ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}/

            cd ${appDir}
            npm install
            npm run build
            sudo fuser -k 3000/tcp || true
            nohup npm run start > /tmp/nextjs-app.log 2>&1 &
            sleep 5
            curl -s -o /dev/null -w "%{http_code}" http://localhost:3000 || echo 'App may still be starting...'
            echo 'Deployment complete - App running on port 3000'
        """
    }
}