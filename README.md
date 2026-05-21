# dotnet-unit-test-xunit


# Tests
This repo demonstrates unit tests using XUnit.  You can run all tests through an IDE like Visual Studio's Test Explorer or via the dotnet cli using the command
```
dotnet test
```
> By default this command will also restore packages and build the solution.  If you do not want to build or restore then use
```
dotnet test --no-restore
```

Tests can be run either for the entire solution for each individual test project.  In the command line simply change the directory to the path containing the .sln or .csproj project file of the test project.  Then run the test command

## Collect Code Coverage - XUnit
The version of Visual studio will determine ways to get code coverage.  By far the easiest way is if using Visual Studio Enterprise as that has the tools and reporting built in.  If using any other version of Visual Studio the following steps will be needed for XUnit

1. Install the report generator as a global tool
```
dotnet tool install -g dotnet-reportgenerator-globaltool
```

2. Navigate to the directory containing the project file `WebApiControllers.XUnit.Tests.csproj`
```
cs <PATH>\WebApiControllers.XUnit.Tests
```
> <PATH> will need to be the location on your local workstation

3. Run the following command to generate Test Results
```
dotnet test --collect:"XPlat Code Coverage"
```
> This will create a folder in the test project named TestResults and it will contain a file named `coverage.cobertura.xml`
> Each time the test command is run to collect code coverage, it will generate a new folder named with a GUID in TestResults.  The GUID folder will contain a file named `coverage.cobertura.xml` and this will be used to generate a more readable html report file in the next step

4. Generate a report from the coverage.cobertura.xml file
```
reportgenerator -reports:"TestResults\<GUID>\coverage.cobertura.xml" -targetdir:"coveragereport" -reporttypes:Html
```
> This will create a folder in the test project named coveragereport.  Open the index.html file in a browser to view coverage results


# References
- [Dotnet CLI](https://learn.microsoft.com/en-us/dotnet/core/tools/)
- [Rob Rich Presentations](https://robrich.org/presentations)
- [Rob Rich XUnit Testing](https://github.com/robrich/net-testing-xunit-moq/blob/main/done/LightController.Tests/LightActuator_ActuateLights.cs)
