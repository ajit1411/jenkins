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
            cd AppCode
            npm run build
            cd ../
            zip app.zip AppCode/build public/web.config
        '''
    }
    stage('Deploy'){
        azureWebAppPublish azureCredentialsId:env.CRED_ID,
        resourceGroup: env.RES_GROUP,
        appName: env.WEB_APP,
        filePath: "**/app.zip"
    }
}