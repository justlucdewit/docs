The following documentation explains step by step how to set up a development environment for business central. This can be either self hosted using a docker image, or using an online sandbox hosted by Microsoft.

<br />

### Installing VSCode
By far the best IDE to use for programming in the AL language (the langauge used by business central) is VS Code, due to the non existing tooling in other IDEs, to the point where you are pracitcally forced to use VSC.

The installation should be very straight forward, but you could use this guide: [[Installing VSCode]]

<br />

### AL vscode extensions
When you have set up visual studio code, and got it running, you want to navigate to the extensions page by pressing the extension icon at the left-side toolbar, or by pressing `ctrl+shift+x`, then search for the extension named 'AL Language' by Microsoft and install it.

![[Pasted image 20221016161120.png]]

Here are some other extensions you might want to install for better quality of life while working with AL:

- AZ AL Dev Tools / AL Code Outline
- Waldo's CRS AL Language Extension
- AL Variable Helper
- Al Object Designer
- AL Extension pack (by waldo)

<br />

### Setting up locally using docker

To install a local development environment via docker, you should first make sure you have installed docker, which you could do via this documentation: [[Installing docker]]

Next up, is pulling a business central image, this can be done using a microsoft tool named the `BcContainerHelper`, to install this run the following commands in a powershell window **with administrator rights**:

```powershell
Install-Module BcContainerHelper -force
Set-ExecutionPolicy RemoteSigned
Import-Module BcContainerHelper
```

Now we can create a new container using the `New-BcContainerWizard` command

This will ask you a bunch of questions on how you want BC to be configured, this should be easy, just make sure to

- dont use windows config
- dont use automated testing
- dont accept includeAL

The `New-BcContainerWizard` will generate a powershell script for you that creates the image. The script with the config that I like to use is:

```powershell
$containerName = 'bcserver'
$password = 'P@ssw0rd'
$securePassword = ConvertTo-SecureString -String $password -AsPlainText -Force
$credential = New-Object pscredential 'admin', $securePassword
$auth = 'UserPassword'
$artifactUrl = Get-BcArtifactUrl -type 'Sandbox' -country 'us' -select 'Latest'
New-BcContainer `
    -accept_eula `
    -containerName $containerName `
    -credential $credential `
    -auth $auth `
    -artifactUrl $artifactUrl `
    -imageName 'mybcimage' `
    -updateHosts

```

This script might give an error that docker is running in linux mode, in that case switch to windows mode like described in [[Installing docker]].

Executing the script might take a while considering it has to pull a base image of 10GB+, this could take up to 10min even on systems with very fast internet speeds

<br />

### Setting up remotely with online sandbox
(this bit of the docs has yet to be written)

