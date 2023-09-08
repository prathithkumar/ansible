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

        stage('Lint Checks'){
            steps {
                sh '''
                    echo ****** Starting Lint Checks *****
                    echo ****** Lint Checks Completed *****
                '''
            }
        }
        stage('Performing a dry run') {           // This stage should run only when we raise a PULL REQUEST
            steps {
                sh '''
                    env
                    ansible-playbook robo-dryrun.yml -e ENV=dev -e COMPONENT=user  -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW}

                '''




            }
        }
    }
}
