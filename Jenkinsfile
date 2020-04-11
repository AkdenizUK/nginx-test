pipeline{
    agent {
        label "generic"
    }
    stages {
        stage ("Create docker image for testing") {
            steps {
                sh """
                    python3 -m molecule create
                """
            }
        }
        stage ("Apply Ansible role to docker image") {
            steps {
                sh """
                    python3 -m molecule converge
                """
            }
        }
        stage ("Check idempotency") {
            steps {
                sh """
                    python3 -m molecule idempotence
                """
            }
        }
        stage ("Cleanup molecule") {
            steps {
                sh """
                    python3 -m molecule cleanup
                """
            }
        }
        stage("Destroy molecule instance") {
            steps {
                sh """
                    python3 -m molecule destroy                       
                """
            }
        }
    }   

}