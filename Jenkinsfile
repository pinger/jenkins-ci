pipeline {
    agent any
    triggers {
    GenericTrigger (
            genericVariables:[
      [key: 'ref', value: '$.ref']
     ],
          causeString: 'Generic Cause',
          token: 'hello',
        )
    }
    parameters {
        string defaultValue: "", description: "refs/heads/main", name: "ref"
    }
    stages {
        stage('Build') {
            steps {
                //
                echo env.ref
            }
        }
        stage('Test') {
            steps {
                //
            }
        }
        stage('Deploy') {
            steps {
                //
            }
        }
    }
}
