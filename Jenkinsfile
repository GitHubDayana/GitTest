pipeline {
    agent any
    environment {
        dotnet = 'C:\\Program Files\\dotnet\\dotnet.exe'
    }
    stages {
        stage('Build Stage') {
            steps {
                bat 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\DemoProject\\DotNetProject\\DotNetProject.csproj --configuration Release'
            }
        }
        stage('Test Stage') {
            steps {
                bat 'dotnet test C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\DemoProject\\DotNetProject\\DotNetProject.csproj'
            }
        }
        stage("Release Stage") {
            steps {
                bat 'dotnet build C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\DemoProject\\DotNetProject\\DotNetProject.csproj /p:PublishProfile=" C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\DemoProject\\DotNetProject\\Properties\\lauchSettings.json" /p:Platform="Any CPU" /p:DeployOnBuild=true /m'
            }
        }
        stage('Deploy Stage') {
            steps {
                //Deploy application on IIS
                bat 'net stop "w3svc"'
                bat '"C:\\Program Files (x86)\\IIS\\Microsoft Web Deploy V3\\msdeploy.exe" -verb:sync -source:package="%WORKSPACE%\\JenkinsWebApplicationDemo\\bin\\Debug\\net6.0\\JenkinsWebApplicationDemo.zip" -dest:auto -setParam:"IIS Web Application Name"="Demo.Web" -skip:objectName=filePath,absolutePath=".\\\\PackagDemoeTmp\\\\Web.config$" -enableRule:DoNotDelete -allowUntrusted=true'
                bat 'net start "w3svc"'
            }
        }
    }
}
