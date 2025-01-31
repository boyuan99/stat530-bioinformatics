# Setting Up Conda in macOS: A Complete Guide

Author: Bo Yuan (boy6@illinois.edu)

Course: STAT 530, Spring 2025

---

This tutorial will walk you through setting up Conda, Miniconda, or Miniforge in macOS using graphical installers.



## Installation Options

### Miniforge (Recommended)
1. Go to: https://conda-forge.org/download/
2. Download the macOS `.pkg` installer:
   - For M1/M2 Macs: `Miniforge3-MacOSX-arm64.pkg`
   - For Intel Macs: `Miniforge3-MacOSX-x86_64.pkg`
3. Double-click the downloaded `.pkg` file
4. Follow the installation wizard
5. Installation directory will be: `~/miniforge3`

### Miniconda (Alternative)

**Anaconda installation is in the same page with Miniconda , don't install the wrong one.**

1. Go to: https://www.anaconda.com/download/success
2. Download the macOS Installer:
   - For M1/M2 Macs: Choose the ARM64 (Apple Silicon) version
   - For Intel Macs: Choose the Intel x86_64 version
3. Double-click the downloaded `.pkg` file
4. Follow the installation wizard
5. Installation directory will be: `~/miniconda3`

### Anaconda (Full Distribution)
1. Go to: https://www.anaconda.com/download/success
2. Download the macOS Installer:
   - The website will automatically detect your system type
3. Double-click the downloaded `.pkg` file
4. Follow the installation wizard
5. Installation directory will be: `~/anaconda3`

## Terminal Integration

After installation, you'll need to set up the terminal:

1. Open Terminal (you can find it in Applications → Utilities → Terminal)

2. Initialize conda:
```bash
conda init "$(basename "$SHELL")"
```

This will add the following initialization block to your shell configuration file:

```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/Users/user_name/miniforge3/bin/conda' 'shell.zsh' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/Users/user_name/miniforge3/etc/profile.d/conda.sh" ]; then
        . "/Users/user_name/miniforge3/etc/profile.d/conda.sh"
    else
        export PATH="/Users/user_name/miniforge3/bin:$PATH"
    fi
fi
unset __conda_setup

if [ -f "/Users/user_name/miniforge3/etc/profile.d/mamba.sh" ]; then
    . "/Users/user_name/miniforge3/etc/profile.d/mamba.sh"
fi
# <<< conda initialize <<<
```

3. To enable automatic activation of the base environment when you open a new terminal:

```bash
conda config --set auto_activate_base true
```
4. Close and reopen Terminal
5. You should see `(base)` at the start of your prompt



## Understanding and Setting Up Your Shell

### Checking Your Current Shell

1. Open Terminal (Applications → Utilities → Terminal)

2. Check which shell you're using:

```bash
echo $SHELL
```

This will show:

- `/bin/zsh` if you're using Zsh (default on macOS Catalina and newer)
- `/bin/bash` if you're using Bash (default on older macOS versions)

### Differences Between Zsh and Bash

1. Configuration Files:
   - Zsh uses: `~/.zshrc`
   - Bash uses: `~/.bash_profile` or `~/.bashrc`

2. Default Prompt:
   - Zsh: `%` symbol
   - Bash: `# Setting Up Conda in macOS: A Complete Guide

### Switching Between Shells

To switch to Bash:

```bash
chsh -s /bin/bash
```

To switch to Zsh:

```bash
chsh -s /bin/zsh
```

After switching:

1. Enter your password when prompted
2. **Close and reopen Terminal**
3. Verify the change: `echo $SHELL`



## Common Errors and Solutions

### Error 1: "conda: command not found"

If you see this error:

```
zsh: command not found: conda
```

**Solution:**

1. Make sure you've completed the installation

2. Open a new Terminal window

3. If the error persists:

   For Zsh users:

   - Open Terminal

   - Open .zshrc file in a text editor:

     ```bash
     nano ~/.zshrc
     ```

   - Add this line at the end of the file:

     ```bash
     export PATH="$HOME/miniforge3/bin:$PATH"  # adjust path if using miniconda3 or anaconda3
     ```

   - Save the file:

     - Press Ctrl + X
     - Press Y to confirm
     - Press Enter to save

   - Apply changes:

     ```bash
     source ~/.zshrc
     ```

   For Bash users:

   - Open Terminal

   - Open .bash_profile:

     ```bash
     nano ~/.bash_profile
     ```

   - Add this line at the end of the file:

     ```bash
     export PATH="$HOME/miniforge3/bin:$PATH"  # adjust path if using miniconda3 or anaconda3
     ```

   - Save the file:

     - Press Ctrl + X
     - Press Y to confirm
     - Press Enter to save

   - Apply changes:

     ```bash
     source ~/.bash_profile
     ```



### Error 2: "mamba not recognized" after Miniforge Installation

If mamba commands don't work after installing Miniforge:

1. Check your conda installation:
```bash
conda env list
```

2. If you see multiple installations like:
```
conda environments:
                         ~/anaconda3
base                  *  ~/miniforge3
```

This means you have multiple conda installations. See the [Managing Multiple Conda Installations](#managing-multiple-conda-installations) section below.



## Managing Multiple Conda Installations

If you have multiple conda installations:

1. Use the macOS System Settings:
   - Open System Settings
   - Go to Applications
   - Search for "conda" or "anaconda"
   - Uninstall any unwanted versions

2. Delete remaining folders if any:
   - Open Finder
   - Press Cmd + Shift + G
   - Type `~/miniforge3` or `~/anaconda3` or `~/miniconda3`
   - Move the unwanted folders to Trash

3. Open a new Terminal window

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

2. Always verify your installation:
   - Open Terminal
   - Type: `conda env list`
   - This should show your base environment



## Setup Environment for the Class

1. Create new environments for different projects:
```bash
conda create -n stat530 python=3.10
```

2. Activate environments:
```bash
conda activate stat530
```

3. Install Jupyter (make sure you are under stat530 environment before you do this):

```bash
pip install jupyter
```



## Apple Silicon (M1/M2) Specific Notes

1. When downloading installers, make sure to choose:
   - ARM64 version for M1/M2 Macs
   - x86_64 version for Intel Macs

2. To check your Mac type:
   - Click the Apple menu () → About This Mac
   - Look for "Chip" or "Processor"
   - M1/M2 = Apple Silicon
   - Intel = Intel processor



## Additional Resources

- Conda documentation: https://docs.conda.io/
- Miniforge GitHub repository: https://github.com/conda-forge/miniforge
- Miniconda documentation: https://docs.conda.io/en/latest/miniconda.html



## Support

If you encounter issues not covered in this guide:
1. Check the conda documentation
2. Run `conda info` in Terminal
3. Look for error messages
4. Check Apple Silicon compatibility if using M1/M2 Mac
5. Consult with TA (Bo Yuan: boy6@illinois.edu)