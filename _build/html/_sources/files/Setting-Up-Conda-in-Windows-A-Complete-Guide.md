# Setting Up Conda in Windows: A Complete Guide

Author: Bo Yuan (boy6@illinois.edu)

Course: STAT 530, Spring 2025

---

This tutorial will walk you through setting up Conda, Miniconda, or Miniforge in Windows, including installation, environment setup, and common troubleshooting steps.



## Table of Contents
1. [Installation Options](#installation-options)
2. [Setting Up PowerShell/CMD Integration](#setting-up-powershellcmd-integration)
3. [Common Errors and Solutions](#common-errors-and-solutions)
4. [Managing Multiple Conda Installations](#managing-multiple-conda-installations)
5. [Best Practices](#best-practices)

 

## Installation Options

### Miniforge (Recommended)
1. Download Miniforge from: https://conda-forge.org/download/
2. Run the installer
3. Installation directory will typically be: `C:\Users\YourUsername\miniforge3`

### Miniconda (Alternative)

**Anaconda installation is in the same page with Miniconda , don't install the wrong one.**

1. Download Miniconda from: https://www.anaconda.com/download/success
2. Run the installer
3. Installation directory will typically be: `C:\Users\YourUsername\miniconda3`

### Anaconda (Full Distribution)
1. Download Anaconda from: https://www.anaconda.com/download/success
2. Run the installer
3. Installation directory will typically be: `C:\Users\YourUsername\anaconda3`



## Setting Up PowerShell/CMD Integration

### Basic Setup

1. Open PowerShell and run:
```powershell
conda init powershell
conda init cmd.exe
```

2. Close and reopen PowerShell/CMD
3. You should see `(base)` at the start of your prompt



## Common Errors and Solutions

### Error 1: "conda not recognized"
If you see this error:
```
conda : The term 'conda' is not recognized as the name of a cmdlet, function, script file, or operable program. Check
the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ conda init powershell
+ ~~~~~
    + CategoryInfo          : ObjectNotFound: (conda:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```

**Solution:**
1. Locate your installation directory (installation_name: miniforge3, miniconda3, or anaconda3)
2. Add these paths to your system environment variables:
   ```
   C:\Users\YourUsername\[installation_name]
   C:\Users\YourUsername\[installation_name]\Scripts
   C:\Users\YourUsername\[installation_name]\Library\bin
   ```

To add environment variables:
1. Right-click "This PC" → Properties
2. Click "Advanced system settings"
3. Click "Environment Variables"
4. Under "System variables", find "Path"
5. Click "Edit" → "New"
6. Add each path
7. Click "OK" to save

### Error 2: "Running Scripts is Disabled"
If you see this error:
```
. : File C:\Users\YourUsername\Documents\WindowsPowerShell\profile.ps1 cannot be loaded because running scripts is disabled
on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:3
+ . 'C:\Users\YourUsername\Documents\WindowsPowerShell\profile.ps1'
+   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

**Solution:**
1. Open PowerShell as **Administrator**
2. Check current policy:
```powershell
Get-ExecutionPolicy
```

3. Set new policy:
```powershell
Set-ExecutionPolicy RemoteSigned
```

4. Type "Y" when prompted
5. Close and reopen PowerShell

### Error 3: "mamba not recognized" after Miniforge Installation

Run:

```bash
mamba --version
```



If you see this error after installing Miniforge:

```
mamba : The term 'mamba' is not recognized as the name of a cmdlet, function, script file, or operable program. Check 
the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ mamba create -n stat530 python=3.10
+ CategoryInfo : ObjectNotFound: (mamba:String) [], CommandNotFoundException
+ FullyQualifiedErrorId : CommandNotFoundException
```

**Solution:**
1. First, check your current conda environments:
```powershell
conda env list
```

If you see multiple base environments like this:
```
conda environments:

base                  *  C:\Users\YourUsername\anaconda3
                         C:\Users\YourUsername\miniforge3
```

This means you have conflicting conda installations. To fix:

1. Deactivate current conda initialization:
```powershell
conda init --reverse
```

2. Update your system environment variables:
   - Open System Properties → Advanced → Environment Variables
   - Under "System Variables", find "Path"
   - Remove any paths containing "anaconda3"
   - Add or ensure these paths exist:
     ```
     C:\Users\YourUsername\miniforge3
     C:\Users\YourUsername\miniforge3\Scripts
     C:\Users\YourUsername\miniforge3\Library\bin
     ```

3. Close and reopen PowerShell

4. Reinitialize conda for Miniforge:
```powershell
conda init powershell
```

5. Close and reopen PowerShell again

6. Verify the correct base environment:
```powershell
conda env list
```

You should now see the Miniforge environment is activated now:
```
conda environments:

base                  *  C:\Users\YourUsername\miniforge3
                         C:\Users\YourUsername\anaconda3
```

7. Now you can use mamba commands:
```powershell
mamba create -n stat530 python=3.10
```

## Managing Multiple Conda Installations

If you have multiple conda installations (e.g., both Anaconda and Miniforge), you might see something like this:
```
# conda environments:
#
base                  *  C:\Users\YourUsername\AppData\Local\anaconda3
env1                     C:\Users\YourUsername\AppData\Local\anaconda3\envs\env1
                        C:\Users\YourUsername\AppData\Local\miniconda3
                        C:\Users\YourUsername\AppData\Local\miniconda3\envs\env2
```

To switch between installations:

1. Deactivate current conda initialization:
```powershell
conda init --reverse powershell
```

2. Remove unwanted installation:
   - Open Windows Settings → Apps & Features
   - Search for the unwanted installation (e.g., "Anaconda")
   - Uninstall
   - Remove remaining directory:
     ```powershell
     Remove-Item -Recurse -Force "C:\Users\YourUsername\AppData\Local\anaconda3"
     ```

3. Initialize desired conda:
```powershell
C:\Users\YourUsername\[installation_name]\Scripts\conda.exe init powershell
```

### Managing Auto-Activation

To disable auto-activation of base environment:
```bash
conda config --set auto_activate_base false
```

To enable auto-activation:
```bash
conda config --set auto_activate_base true
```

## Best Practices

1. Choose one conda distribution and **stick with it**:
   - Miniforge: If you want conda-forge as default channel + mamba
   - Miniconda: If you want minimal installation
   - Anaconda: If you want full scientific distribution

2. Always check your environment before creating new ones:
```powershell
conda env list
where conda
```

3. Close and reopen terminals after making environment changes

4. Use `RemoteSigned` execution policy for balance of security and usability

5. Keep track of your environment locations

6. Regularly check `conda env list` to understand your setup



## Setup Environment for the Class

1. Create new environments for different projects:
```bash
conda create -n stat530 python=3.10
```

2. Activate environments:
```bash
conda activate stat530
```



## Additional Resources

- Conda documentation: https://docs.conda.io/

- Miniforge GitHub repository: https://github.com/conda-forge/miniforge

- Miniconda documentation: https://docs.conda.io/en/latest/miniconda.html

  

## Support

If you encounter issues not covered in this guide:
1. Check the conda documentation
2. Run `conda info` for system information
3. Look for error messages in the conda output
4. Consult with TA (Bo Yuan: boy6@illinois.edu)

