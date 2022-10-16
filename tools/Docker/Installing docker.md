### Docker desktop installer
First off, download the docke-desktop installer at [their website](https://www.docker.com/)

After installation, please make sure that your Docker is running in Windows container Mode, To check that, in the tray bar, right click on the Docker icon and check if you ahve the option `Switch to Linux containers`. If yes, then it means that your docker works as windows containers. You can also mark this option during the installation.

Once it is installed, you are going to have to shutdown and restart your system.

<br />

### Docker CLI
You could also install docker without the desktop part, so you can use it via just the CLI, to do this, open a powershell window as administrator, and run the following commands:

```powershell
Install-Module DockerMsftProvider -Force
Install-Package Docker -ProviderName DockerMsftProvider -Force
```

<br />

### Test if installation succeeded
To test if the installation was successfull you could run the following command that runs a test container, in powershell:

```powerhsell
docker container run -r hello-world
```

![[Pasted image 20221016180125.png]]

<br />

### Error: hardware assisted virtualization and data execution protection must be enabled in the BIOS. See https://docs.docker.com/desktop/windows/troubleshoot/#virtualization

When you get this error after restarting, the first step will be [[Opening the bios]].

After you have done that, you have to find some option about enabeling virtualization in your CPU. Where this is located can defer based on your specific CPU and Bios.

<br />

### Error: docker: error during connect: This error may indicate that the docker daemon is not running.
When you get this error while trying out the hello-world container, you have to open docker desktop, and you will notice that its not running, this could be due to an error that you might get in a popup, that states that `WSL 2 installation is incomplete`.

This can be fixed using the following [guide](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package).

1) Enable WSL using `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart` in powershell.
2) Enable VM feature using `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart` in powershell
3) Download and install the [linux kernel update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).
4) Close and restart docker desktop.