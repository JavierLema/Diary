---
tags: [TIPS]
title: Unit tests
created: '2024-12-18T09:52:43.097Z'
modified: '2024-12-18T12:02:39.466Z'
---

# Unit tests

### IMPORTANT NOTES
- If you create a new proyect with unit tests, you need to add dll at:
  - RunUnitTests.ps1
  - SonarQube-Analyze.ps1

#### xUnit samples

- Example to create two unitary tests and check the result is false.
  ```
  [Theory]
  [InlineData("hi, this, is, another, tag, list")]
  [InlineData("hi this is; multiple,tag,list")]
  public void InvalidCharacters(string tag)
  {
    LibImportRecord libImport = GetLibImportRecord(tag);

    // Assert
    Assert.False(libImport.HasInvalidTags());
  }
  ```
#### How to test?
using the command: **dotnet vstest test.dll**
