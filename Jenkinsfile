properties([
    pipelineTriggers([[$class: 'GitHubPushTrigger']])
])

node {
        stage('Define env variables'){
        env.GIT_BRANCH = 'refs/heads/feature-ci-pipeline' 
        env.PATH_TO_PROJECT_FILE = "C:\\Users\\jenkins\\Documents\\SUContent-SEDO-Regular-Exam-2024-10-2\\Homies.sln"
        env.PATH_TO_UNIT_TESTS = "C:\\Users\\jenkins\\Documents\\SUContent-SEDO-Regular-Exam-2024-10-2\\Homies.UnitTests\\Homies.UnitTests.csproj"
        env.PATH_TO_INTEGRATION_TESTS = "C:\\Users\\jenkins\\Documents\\SUContent-SEDO-Regular-Exam-2024-10-2\\Homes.IntegrationTests\\Homes.IntegrationTests.csproj"
        }

        stage('Clean Working Space') {
            cleanWs()
        }

        stage('Restore Project Packages') {
            bat "dotnet restore %PATH_TO_PROJECT_FILE%"
            echo "Package restore done!"
        }

        stage('Build the Project') {
            bat "dotnet build %PATH_TO_PROJECT_FILE%"
            echo "Project build done!"
        }

        stage('Run Both Integration and Unit Tests on branch feature-ci-pipeline') {
            bat """
            dotnet test %PATH_TO_UNIT_TESTS% --configuration Release
            dotnet test %PATH_TO_INTEGRATION_TESTS% --configuration Release
            echo Tests completed!
            """
        }
}