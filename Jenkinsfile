pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build stage (listing files)'
                sh 'ls -la'
            }
        }

        stage('Test') {
    steps {
        echo 'Running calculator tests...'

        sh '''
        python3 - <<EOF
import calculator

assert calculator.add(2,3) == 5
assert calculator.sub(5,2) == 3
assert calculator.mul(3,4) == 12
assert calculator.div(10,2) == 5

print("All tests passed!")
EOF
        '''
    }
}
        stage('Deploy') {
            steps {
                echo 'Deployment stage (simulated)'
                echo 'Application deployed successfully!'
            }
        }
    }
}
