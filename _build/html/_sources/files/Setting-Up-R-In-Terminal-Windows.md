# Setting Up R in Terminal (Windows) and Jupyter

**Author**: Bo Yuan (boy6@illinois.edu)

**Course**: STAT 530, Spring 2025

>This guide covers setting up R in **Windows terminal** (PowerShell, CMD). This setup is **optional** but potentially helpful for future study.
>
>Note for macOS users: After installing R, terminal setup is usually automatic. Contact TA if you encounter issues.



## Initial Installation

1. Download R from the [CRAN website](https://cran.r-project.org/)
2. For Windows users, select and install the `.exe` file with default settings
3. Make sure to check "Add R to system PATH" during installation



## Verifying Installation
Open PowerShell and run:
```powershell
R --version
```



## Running R in Windows PowerShell

- **Start R Interactive Mode**: Type `R` and press Enter
- **Run R Scripts**: Use `Rscript script.R` to execute R files



## Troubleshooting Common Issues

### Path Configuration
If R command is not found:
1. Add R installation path to system environment variable `Path`
2. Typical path: `C:\Program Files\R\R-x.x.x\bin` (replace x.x.x with your R version)
3. Verify path with: `$env:Path` in PowerShell



### PowerShell Alias Conflict

#### Check for Alias

First, check if 'r' is already defined as an alias:

```powershell
Get-Alias r
```

If you see the following output, there's an alias conflict:

```
CommandType     Name                Version    Source
-----------     ----                -------    ------
Alias           r -> Invoke-History
```

Note: Typically it's `Invoke-History`, but could be different if you've set custom aliases.

#### Remove Alias 

⚠️ Only proceed if you don't need `r` for `Invoke-History`:

```powershell
Remove-Item Alias:r
```



### Alternative Direct Execution
If alias issues persist, you can directly call R.exe:
```powershell
& "C:\Program Files\R\R-x.x.x\bin\R.exe"
```
(Replace x.x.x with your actual R version)



## Setting Up R in Jupyter Notebook

### Prerequisites

1. Make sure you have  Jupyter Notebook installed
2. R must be properly installed on your system (follow steps above)

### Installation Steps

1. **Install IRkernel**
   Open R and run these commands:

   ```R
   install.packages('IRkernel')
   IRkernel::installspec()
   ```

2. **Verify Installation**

   - Launch Jupyter Notebook:

     ```bash
     jupyter notebook
     ```

   - Click "New" and verify that "R" appears in the dropdown menu



### Troubleshooting Jupyter Integration

If R kernel doesn't appear:

1. Ensure R installation is in system PATH
2. Try running IRkernel installation with admin privileges
3. Restart Jupyter Notebook after installation

Common Issues:

- If you see "kernel not found" errors, reinstall IRkernel

- For package installation errors, try:

  ```R
  install.packages('IRkernel', repos='http://cran.us.r-project.org')
  ```
