pipeline{
    agent any

    stages{
        stage("Start Grid"){
            steps{
                bat "docker-compose -f grid.yaml up --scale chrome=1 --scale firefox=1 -d"
            }
        }
        stage("Execute Test Suites"){
            steps{
                bat "docker-compose -f features.yaml up"
            }
        }
        }

    post{
        always{
            bat "docker-compose -f grid.yaml down"
            bat "docker-compose -f features.yaml down"
            archiveArtifacts artifacts: 'docker-output/results.html', followSymlinks: false
            archiveArtifacts artifacts: 'docker-output/testLogs.log', followSymlinks: false
        }
    }
}