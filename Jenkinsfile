node{
    stage('init'){
        echo "initializing the pipeline"
    }
    stage('Dependencies Installation'){
        sh '''
            npm install
        '''
    }
    stage('Building artifact'){
        sh '''
            npm run build
            zip app.zip build public/web.config
        '''
    }
    stage('Deploy'){
        azureWebAppPublish azureCredentialsId:env.CRED_ID,
        resourceGroup: env.RES_GROUP,
        appName: env.WEB_APP,
        filePath: "**/app.zip"
    }
}