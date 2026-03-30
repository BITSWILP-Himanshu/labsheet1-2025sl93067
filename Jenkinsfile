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
assert calculator.subtract(5,2) == 3
assert calculator.multiply(3,4) == 12
assert calculator.divide(10,2) == 5

print("All tests passed!")
EOF
        '''
    }
}
       
stage('Deploy') {
    steps {
        echo 'Deploying to AWS EC2...'

        sshagent(credentials: ['aws-ec2-key']) {
            sh '''
            scp -o StrictHostKeyChecking=no calculator.py ubuntu@16.171.21.53:/home/ubuntu/

            ssh -o StrictHostKeyChecking=no ubuntu@16.171.21.53 "ls -l /home/ubuntu/"
            '''
        }
    }
}

}
