# Overview

This repository serves as a minimal reproduction for a bug I found with Source Generators.


# Steps

- Run `dotnet build` in the `src` folder
- In `src\TestGenerator\TestGenerator.cs` change the type name from `TestGenerator1` to `TestGenerator2`
- Run `dotnet clean` in the `src` folder (otherwise the  build does not re-run)
- Run `dotnet build` in the `src` folder

# Expected result

- The build finishes without a warning

# Actual result 

- There is a warning:
```
CSC : warning CS8032: An instance of analyzer TestGenerator.TestGenerator2 cannot be created from <localPath>\src\TestGenerator\bin\Debug\netstandard2.0\TestGenerator.dll : Could not load type 'TestGenerator.TestGenerator4' from assembly 'TestGenerator, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null'.. [<localPath>\src\TestGenerator.Tests\TestGenerator.Tests.csproj]
```
- When I manually check the dll in the location via ILSpy, the requested type is there
