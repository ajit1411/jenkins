node{
    stage('init'){
        echo "initializing the pipeline"
        checkout scm
    }
    stage('Dependencies Installation'){
        sh '''
            ls -l
            cd AppCode/
            npm install
        '''
    }
    stage('Building artifact'){
        sh '''
            cd AppCode
            npm run build
            cd ../
            zip app.zip AppCode/build AppCode/public/web.config
        '''
    }
    stage('Deploy'){
        azureWebAppPublish azureCredentialsId:env.CRED_ID,
        resourceGroup: env.RES_GROUP,
        appName: env.WEB_APP,
        filePath: "app.zip",
        sourceDirectory: '/var/lib/jenkins/workspace/mytodoapp/',
        targetDirectory: '/wwwroot'
    }
}