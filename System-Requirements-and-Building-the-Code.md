* [System Requirements](#system-requirements)
* [Folder Layout](#folder-layout)
* [Running SHFB and the Sandcastle Tools with the Source Code Version](#running-shfb-and-the-sandcastle-tools-with-the-source-code-version)
* [Building and Debugging the Projects](#building-and-debugging-the-projects)

## System Requirements
In order to use Sandcastle and the Sandcastle Help File Builder (SHFB) you will need the following tools:

Required:
* .NET Framework 4.7.2 or later (Needed to run the Sandcastle and SHFB tools)

Optional:
* HTML Help Workshop (Used for building Help 1 CHM files)

In order to build the source code you will need the following tools:

Required:
* Visual Studio 2022 or later (Used to build the C# projects for the tools)

Optional:
* Visual Studio extension development workload for your version of Visual Studio.  Required for VSPackage development.
* Wix 3.x Toolset.  Used to create the MSI installer.

## Folder Layout
*Deployment* - This folder contains the deployment resources (the installer and all related files).  These are
used when creating the distribution package for SHFB.

*Documentation* - This folder contains documentation projects for Sandcastle and SHFB as well as related
documentation projects for such things as the MAML Guide.

*SHFB\Deploy* - This folder contains some supporting files and will contain the SHFB and the Sandcastle tools
and their configuration files once they are built.  All of the projects place their build output here so that
the entire toolset can be tested in a common location that matches the release build folder layout.  Some of the
key folders beneath it are listed below.  See the [build engine](http://ewsoftware.github.io/SHFB/html/ede54bc8-7027-48be-ba0c-66d8f24bdccd.htm)
help topic for a description of the subfolders and their content.

*SHFB\Source* - This folder contains the source code for SHFB and the Sandcastle tools.  All output is sent to
the *SHFB\Deploy* folder.  Some aggregate solutions exist in this folder that can be used to load groups of
related projects.  The individual Sandcastle tool projects have their own solution files in their project
folders to allow working with them individually as well.

*TestCaseProject* - This folder contains a test project with various test cases and test documentation projects.

## Running SHFB and the Sandcastle Tools with the Source Code Version
When you install SHFB and the Sandcastle tools, it creates a system environment variable called `SHFBROOT` that
points to the release version (typically *C:\Program Files (x86)\EWSoftware\Sandcastle Help File Builder*).  To
use the source code version of the tools, you must edit your system environment variables to point `SHFBROOT` at
the *SHFB\Deploy\\* folder of the source code installation.  For example, set it to *C:\GH\SHFB\SHFB\Deploy\\*.
Your location may differ based on where you extracted the code.  This will allow you to run the source code
version of the tools while leaving the release build in place in the standard location.  You can freely make
changes to the tool source code and presentation style files and test them as needed.  Pointing `SHFBROOT` back
at the standard location for the release version of the tools will let you run it to compare the results against
your changed version.

Before using the source code version, you will need to build the tools and the reflection data files.  To do
this, open a command prompt, change into the root folder, and run the *MasterBuild.bat* script.  This will build
the tools and place them in the *SHFB\Deploy* folder ready for use.  By default, the Release version is built.
To build a debug version, pass in the command line parameter *Debug*.  As noted above, the script will generate reflection data for the latest version of the `.NETFramework` platform based on the versions available on your system.  The reflection data files will be placed in the *.\Deploy\Data\\.NETFramework* folder.  To build reflection data for other platforms such as `.NETCore`, `.NETPortable`, `.NETMicroFramework`, `Silverlight`, `WindowsPhone`, and `WindowsPhoneApp`, see the *Reflection Data Manager* topic in the Sandcastle Tools help file.

As an alternative, you can copy the reflection data folders from the installed release version of the Sandcastle Help File Builder or extract them from the related NuGet packages and copy them to the locations noted above.

## Building and Debugging the Projects
To build the projects, open the solution file (_\*.sln_) found in the *SHFB\Source\\* folder and build it.  Solution files for the individual projects can be found in each of the subfolders in the event you want to work on just one of the tools.  You can also run the *MasterBuild.bat* script from a command prompt to build the project as noted above.

In order to debug the VSPackage project (*VSIX_2017.sln* or *VSIX_2022.sln*):

* Set the *SandcastleBuilderPackage* project as the default project and then open its project properties.
* Go to the **Debug** category.
* For the **Start Action** option, set it to **Start external program**, click the "..." button after the text
box, navigate to the installation folder for your version of Visual Studio and select the *devenv.exe* file in
that folder (i.e. *C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\devenv.exe*).
* For the **Command line arguments** option, enter the value `/rootsuffix Exp`.
* When you run the project, it should start a new instance of Visual Studio using the experimental instance
settings.
