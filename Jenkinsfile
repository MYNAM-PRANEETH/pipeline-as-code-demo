
pipeline {

    agent {
        node {
            label 'SLAVE01'
        }
    }

    tools { 
        maven 'maven3' 
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '15', 
                    numToKeepStr: '10'
            )
    }

    environment {
        APP_NAME = "DCUBE_APP"
        APP_ENV  = "DEV"
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace for ${APP_NAME}"
                """
            }
        }

        stage('Code Checkout') {
    steps {
        tool 'Default'
        checkout([
            $class: 'GitSCM', 
            branches: [[name: '*/master']], 
            userRemoteConfigs: [[url: 'https://github.com/MYNAM-PRANEETH/pipeline-as-code-demo.git']]
        ])
    }
}



       stage('Code Build') {
    steps {
        tool 'maven3'
        sh 'mvn install -Dmaven.test.skip=true'
    }
}


        stage('Priting All Global Variables') {
            steps {
                sh """
                env
                """
            }
        }

    }   
}
