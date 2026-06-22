### Tips & Tricks for MSBuild
📌 Using macros to customize the location of output files.
```xml
<ItemGroup>
    <None Include="wwwroot\**\*" CopyToOutputDirectory="PreserveNewest"/>
    <None Include="wwwroot\**\*"  Link="wwwroot\%(RecursiveDir)%(Filename)%(Extension)" CopyToOutputDirectory="PreserveNewest"/>
	<EmbeddedResource Include="..\scripts\**\*" LogicalName="scripts/%(RecursiveDir)%(Filename)%(Extension)" Visible="false" />
</ItemGroup>
```

---
📌 Uses `Directory.Build.props` to define the location of the intermediate build artifacts (`obj`) folder.
```xml
<Project>
    <PropertyGroup>
		<!-- Note for BaseIntermediateOutputPath:
		BaseIntermediateOutputPath defines the location for intermediate build artifacts (obj folder).
		BaseIntermediateOutputPath does not support relative path, so we need to get drive root (Ex: "E:\").
		-->
		<DirectoryRoot>$([System.IO.Path]::GetPathRoot($(SolutionDir)))</DirectoryRoot>
<BaseIntermediateOutputPath>$(DirectoryRoot)output\$(SolutionName)\$(MSBuildProjectName)\obj\</BaseIntermediateOutputPath>
    </PropertyGroup>
</Project>
```
Use this together with `BaseOutputPath` to keep your project folder tree clean and organized.
```xml
<BaseOutputPath>\output\$(SolutionName)\$(MSBuildProjectName)</BaseOutputPath>
```

---
📌 Use MSBuild conditions to target multiple platforms.

```xml
<Choose>
	<When Condition="'$(TargetFramework)' == 'net10.0-windows'">
		<PropertyGroup>
			<UseWindowsForms>true</UseWindowsForms>
			<DefineConstants>$(DefineConstants);NET10_0_WINDOWS</DefineConstants>
		</PropertyGroup>
		<ItemGroup>

		</ItemGroup>
	</When>
</Choose>
```
## 📒 External Links
[Common macros for MSBuild commands and properties](https://learn.microsoft.com/en-us/cpp/build/reference/common-macros-for-build-commands-and-properties) 

[Property functions for MSBuild](https://learn.microsoft.com/en-us/visualstudio/msbuild/property-functions)

[MSBuild conditions](https://learn.microsoft.com/en-us/visualstudio/msbuild/msbuild-conditions)