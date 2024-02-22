@Library('goat-shared-library') _

properties(
    [buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')), 
    parameters(
        [string(defaultValue: '', description: 'Ex: iad2apbclusXbr0.iad2.objectrocket.com,iad2apbclusXbr1.iad2.objectrocket.com,iad2apbclusXbr2.iad2.objectrocket.com', name: 'hostnames', trim: true)]
    ), 
    [$class: 'ThrottleJobProperty', categories: [], limitOneJobWithMatchingParams: false, maxConcurrentPerNode: 0, maxConcurrentTotal: 0, paramsToUseForLimit: '', throttleEnabled: false, throttleOption: 'project']]
)

pipeline {
    agent {
        node {
            label 'docker-agent-ansible-python'
        }
    }


    stages {
        // Access the input value in each stage using env.MY_STRING
        stage('Validate Inputs') {
            steps {
                echo "Received Hostnames: ${env.HOSTNAMES}"
                // Do something with the string
                script {
                    common.validateInput("${env.HOSTNAMES}")
                    if (env.ISABORT.toBoolean()) {
                        echo "Hostname Validation Failed"
                        currentBuild.result = 'FAILURE'
                        sh returnStatus: 0, script: 'exit 0'
                    }
                }
            }
        }

        stage('Bootstrap') {
            steps {
                echo "Processed string in Stage 1: ${env.CUSTOMER}"
                // Use the processed string in Stage 2
                script {
                    // Example: Send the string to another system
                    mongod.bootstrap()
                }
            }
        }
    }
}
