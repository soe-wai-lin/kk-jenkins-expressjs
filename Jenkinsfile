pipeline {
    // agent {
    //     label 'Jenkins-Agent'
    // }

    agent any
    
    tools {
        nodejs 'nodejs-22.6.0'  
    }

    stages {
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
                dependencyCheck additionalArguments: '''--scan express-repo/examples/hello-world
                --format XML''', odcInstallation: 'OWASP-DepCheck-10'
            }
        }
    }
    
}
