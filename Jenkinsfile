pipeline {
    // agent {
    //     label 'Jenkins-Agent'
    // }

    agent any
    
    tools {
        nodejs 'nodejs-22.6.0'  
    }

    stages {
        stage('checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/soe-wai-lin/kk-jenkins-expressjs.git']])
            }
        }
        
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
    
    
        stage('NPM test') {
            steps {
                sh '''
                    npm test
                    echo $?
                '''
            }
        }

        // stage('Code Coverage') {
        //     steps {
        //         catchError(buildResult: 'SUCCESS', message: 'Oops! please fix next', stageResult: 'UNSTABLE') {
        //             sh '''
        //                 npm run coverage
        //                 echo $?
        //             '''
        //         }
        //     }
        // }


        
        stage('owasp') {
            steps {
                dependencyCheck additionalArguments: '''--scan /home/sysadmin/workspace/essjs-org_kk-expressjs_expressjs/
                --format XML''', odcInstallation: 'OWASP-DepCheck-10'
            }
        }
    }
    
}
