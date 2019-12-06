pipeline{
    agent any

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
        }
    }
}