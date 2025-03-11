# Xilinx ISE Design Suite 14.7 Installation Guide for Windows 10/11

This guide explains how to install and run Xilinx ISE Design Suite 14.7 on Windows 10/11 without using VirtualBox (VM). Tested on Windows 11.  
*Note: This guide has not attempted to compile to hardware (FPGA)*

---

## Installation Steps

### 1. Download the Installation Files

- Download this repository.
- Download the Xilinx ISE Design Suite 14.7 installation file from [here](https://account.amd.com/en/forms/downloads/xef.html?filename=Xilinx_ISE_DS_Win_14.7_1015_1.tar) and extract the contents.

### 2. Run the Installer

- Open the extracted folder and run `xsetup.exe`.
- During the installation, choose **ISE WebPACK Edition** and leave other options as default.

### 3. Handle Installation Hang at 91%

If the installation gets stuck at 91% with a message like "Enable WebTalk to send...":

- Open **Task Manager** (Ctrl + Shift + Esc).
- Find the `xwebtalk.exe` process (it should be below other Xilinx-related processes).
- Right-click it and select **End Task**.

### 4. Finish Installation

After ending the `xwebtalk.exe` task, the installation should complete. Do not open the software yet.

---

## Post-Installation Configuration

### 1. Add System Environment Variable

- Open **Control Panel > System and Security > System > Advanced System Settings > Advanced > Environment Variables**.
- Add a new **System Variable** with the following values:
  - **Variable Name:** `XILINX_VC_CHECK_NOOP`
  - **Value:** `1`

This will suppress the error message related to **VC++ 2008**.

### 2. Replace Missing Files (`libPortability.dll`)

Download the **Xilinx ISE Win10 Hotfix** from [here](https://support.xilinx.com/s/question/0D52E00006lkXaASAU/installation-of-ise-webpack-on-windows-11?language=en_US) (or similar repository). Then, replace the following files:

- **For 32-bit systems:**
  - Copy `nt\libPortability.dll` from the hotfix folder to the following locations:
    - `C:\Xilinx\14.7\ISE_DS\ISE\lib\nt\libPortability.dll`
    - `C:\Xilinx\14.7\ISE_DS\common\lib\nt\libPortability.dll`

- **For 64-bit systems:**
  - Copy `nt64\libPortability.dll` from the hotfix folder to the following locations:
    - `C:\Xilinx\14.7\ISE_DS\ISE\lib\nt64\libPortability.dll`
    - `C:\Xilinx\14.7\ISE_DS\common\lib\nt64\libPortability.dll`

### 3. Launch Xilinx ISE

After performing the above steps, you should be able to run Xilinx ISE. When prompted for a license, refer to this [YouTube video](https://www.youtube.com/watch?v=VMEIPCjqinA&ab_channel=LaurenceGregg) (skip to minute 7:05) for assistance.

---

## Troubleshooting ISim Simulator

When running ISim simulation, you might encounter an issue where the process hangs during "Elaborating," followed by a failure message. To resolve this:

1. Navigate to the `isim` folder within your project.
2. Locate the file matching the naming convention: `<module_name>_isim_<model_type>...exe.sim`.
3. Replace the `libPortability.dll` in the `nt64` directory (or `nt` for 32-bit systems) with the one from the corresponding directory in the hotfix folder.
4. After replacing the file, try running the simulation again.

This should resolve the issue.

---

## References

- [Installation of ISE WebPACK on Windows 11](https://support.xilinx.com/s/question/0D52E00006lkXaASAU/installation-of-ise-webpack-on-windows-11?language=en_US)
- [How to Work with Xilinx ISE 14.7 in Windows 11](https://support.xilinx.com/s/question/0D52E00006vz7tSSAQ/how-to-work-xilinx-ise-147-in-window-11?language=en_US)
- [YouTube Video for License Setup](https://www.youtube.com/watch?v=VMEIPCjqinA&ab_channel=LaurenceGregg)
