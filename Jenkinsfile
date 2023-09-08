pipeline {
    agent any

    environment{
        SSH_CRED = credentials('SSH_CRED')                                           // Pipeline Variables: ALL the stages of the pipeline can use it.
    }

    // parameters {
    //      string(name: 'PERSON', defaultValue: 'mongodb' , description: 'Enter the componenty name')
    //       choice(name: 'CHOICE', choices: ['dev','prod'],description: 'choose the env')
    // }
    
    stages {

        stage('Lint Checks'){                      // // This stage will only be executed when you run the job from a feature branch 
            when { branch 'master' }
            steps {
                sh '''
                    env
                    echo ****** Starting Lint Checks *****
                    echo ****** Lint Checks Completed *****
                '''
            }
        }
        stage('Performing a dry run') {           // This stage should run only when we raise a PULL REQUEST
            steps {
                sh '''
                    env
                    # ansible-playbook robo-dryrun.yml -e ENV=dev -e COMPONENT=user  -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}

                '''
            }
            
        }

        stage('Main Branch'){                      // // This stage will only be executed when you run the job from a feature branch
            when { branch 'main' } 
            steps {
                sh '''
                    env
                    echo Name of the branch job running against is ${BRANCH_Name}
                '''
            }
        }
    }
}
