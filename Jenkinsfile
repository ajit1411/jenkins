node{
    stage('Git Checout'){
        echo "initializing the pipeline"
        checkout scm
    }
    stage('Dependency Installation'){
        sh '''
            ls -l
            cd AppCode/
            npm install
        '''
    }
    stage('Building Artifact'){
        sh '''
            cd AppCode
            npm run build
            cd ../
            cp index.js AppCode/build
        '''
    }
    stage('Deploy Artifact'){
        azureWebAppPublish azureCredentialsId:env.CRED_ID,
        resourceGroup: env.RES_GROUP,
        appName: env.WEB_APP,
        sourceDirectory: '/var/lib/jenkins/workspace/mytodoapp/AppCode/build',
        targetDirectory: 'react'
    }
}