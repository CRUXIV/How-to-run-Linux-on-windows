# Run Linux Applications on Windows with WSL

This repository contains a PowerShell script to set up and configure Windows Subsystem for Linux (WSL) on Windows. This setup allows you to run Linux applications directly from within Windows.

## How to Set Up the Script

Follow these steps to install and configure WSL, and then use the provided PowerShell script to run Linux applications from Windows:

### 1. Install WSL and a Linux Distribution

1. **Run the Script**

   Open PowerShell as Administrator and create a new script file:

    ```powershell
    nano ~/setup_wsl.ps1
    ```

   Copy and paste the following content into `setup_wsl.ps1`:

    ```powershell
    # Check if WSL is installed
    $wslStatus = wsl --status
    if ($wslStatus -match "WSL version: (.*)") {
        Write-Host "WSL is already installed."
    } else {
        # Install WSL
        Write-Host "Installing WSL..."
        wsl --install
    }

    # Ensure WSL is using version 2
    Write-Host "Setting WSL to version 2..."
    wsl --set-default-version 2

    # Check if Ubuntu is installed
    $ubuntuStatus = wsl -l -v | Select-String -Pattern "Ubuntu"
    if ($ubuntuStatus) {
        Write-Host "Ubuntu is already installed."
    } else {
        Write-Host "Installing Ubuntu..."
        wsl --install -d Ubuntu
    }

    # Create a function to run Linux GUI apps
    Write-Host "Creating Linux app launcher function..."
    Function Start-LinuxApp {
        param (
            [string]$appName
        )
        wsl -e bash -c "$appName"
        Write-Host "$appName is running in WSL."
    }

    # Example usage: Start-LinuxApp "firefox"
    ```

   Save the file and exit the editor:
    - Press `Ctrl + X`
    - Press `Y` to confirm saving
    - Press `Enter` to exit

2. **Make the Script Executable**

   To execute the script, use the following command in PowerShell:

    ```powershell
    ~/setup_wsl.ps1
    ```

### 2. Using the Script

After running the script:

1. **Launch Linux Apps**

   You can launch any Linux application installed in your WSL environment from PowerShell using the function provided in the script. For example:

    ```powershell
    Start-LinuxApp "firefox"
    ```

   This command will run `firefox` in your WSL environment.

## Notes

- Ensure you have installed any required Linux applications in your WSL environment using the Linux package manager.
- The script sets WSL to version 2, which supports GUI applications.

## License

This project is licensed under the MIT License.

## Contact

For any questions or issues, please contact [your-email@example.com].
