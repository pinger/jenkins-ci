pipeline {
    agent any
    triggers {
    GenericTrigger (
            genericVariables:[
                [key: 'ref', value: '$.ref'],
                [defaultValue: '', key: 'repo_name', regexpFilter: '', value: '$.repository.name'],
                [defaultValue: '', key: 'repo_url', regexpFilter: '', value: '$.repository.clone_url'],
                [defaultValue: '', key: 'sender_email', value: '$.sender.email'],
     ],
          causeString: 'Generic Cause',
          token: 'hello',
        )
    }
    parameters {
        string 'repo_name'
        string 'repo_url'
        string defaultValue: "", description: "refs/heads/main", name: "ref"
    }
    stages {
        stage('Git Pull') {
            steps {
               ws("${repo_name}") {
                   cleanWs()
                   checkout scm: [$class: 'GitSCM',
                          branches: [[name: "${ref}"]],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'SubmoduleOption',
                                disableSubmodules: false,
                                parentCredentials: false,
                                recursiveSubmodules: true,
                                reference: '',
                                trackingSubmodules: false]], 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[url: "${repo_url}"]]],
                        poll: false
                }
            }
        }
        stage('Build') {
            steps {
                ws("${repo_name}") {
                    //cat README.md
                    sh """
                        pwd
                        ls -lcha
                    """
                }
            }
        }
        stage('Test') {
            steps {
                ws("${repo_name}") {
                    sh """
                        cat README.md
                    """
                }
            }
        }
        stage('Deploy') {
            steps {
                //
                echo env.ref
            }
        }
    }
    post {
        always {
            script{
                cleanWs()
           }
       }
    }
}
