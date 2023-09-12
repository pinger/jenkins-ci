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
                    git branch: "${ref}",
                    url: "${repo_url}",
                    changelog: false,
                    poll: false
                }
            }
        }
        stage('Build') {
            steps {
                ws("${repo_name}") {
                    cat README.md
                }
            }
        }
        stage('Test') {
            steps {
                //
                echo env.ref
            }
        }
        stage('Deploy') {
            steps {
                //
                echo env.ref
            }
        }
    }
}
