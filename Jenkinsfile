pipeline{
    agent any
    stages{
        stage('Build'){
            when{
                branch 'master'
            }
            steps{
                sh "dotnet restore"
                sh "dotnet build"
                sh "dotnet publish -c release -o ./Output"
            }
        }

        stage('Test'){
            when{
                branch 'dev'
            }
            steps{
                sh "dotnet restore"
                sh "dotnet build"
                sh "dotnet publish -c release -o ./Output"
                sh "dotnet test --logger 'trx;LogFileName=test1.trx' -r ./Output/Results/"
                mstest testResultsFile:"**/*.trx", keepLongStdio: true
            }
        }
        stage('Rsync'){
            when{
                branch 'master'
            }
            steps{
                sh "rsync -a /var/lib/jenkins/workspace/netcoreAPI_master/Output/ nucleus@localhost:/home/nucleus/myNetCoredll"
            }
        }
    }
}