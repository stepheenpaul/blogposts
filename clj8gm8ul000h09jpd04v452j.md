---
title: "Resolving the 'sequelize Running Script Disabled' Error with a Single Command!"
seoTitle: "Troubleshooting 'sequelize' Error: Enabling Script Execution"
seoDescription: "Follow our step-by-step guide to change the execution policy in PowerShell, allowing you to resolve sequelize Running Script Disabled' Error."
datePublished: Fri Jun 23 2023 10:59:11 GMT+0000 (Coordinated Universal Time)
cuid: clj8gm8ul000h09jpd04v452j
slug: resolving-the-sequelize-running-script-disabled-error-with-a-single-command
tags: postgresql, security, nodejs, sequelize, powershell

---

I have been in the process of setting up the server side of a node js project. I am using PostgreSQL with my ORM as Sequelize when I came across this error message.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687517278615/cf1b799b-7d04-4f99-9f5b-dbc47e511216.png align="center")

The error message indicates that there is a problem with running scripts in PowerShell on your system. It specifically mentions that running scripts is disabled, which is why the file "sequelize.ps1" cannot be loaded. This error is related to the execution policy set in PowerShell.

The execution policy is a security feature in PowerShell that determines whether scripts can be run and what types of scripts are allowed. By default, PowerShell has a restricted execution policy, which prevents the execution of scripts.

To resolve this issue, you can try changing the execution policy to allow script execution. Here's how you can do it:

1. Open PowerShell as an administrator. Right-click on the PowerShell icon and select "Run as administrator."
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687517500453/53b47872-9c66-4675-bd22-41e0db5d8681.png align="center")
    
2. In the administrator PowerShell window, run the following command:
    
    ```bash
    Set-ExecutionPolicy RemoteSigned
    ```
    
    This command sets the execution policy to "RemoteSigned," which allows the execution of locally created scripts but requires downloaded scripts to be signed.
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687517560752/5bed72f4-f451-43d7-9b3f-750cda960e5a.png align="center")
    
3. When prompted to confirm the change, type "Y" and press Enter.
    
    After changing the execution policy, try running the "sequelize init" command again. It should now be able to load the "sequelize.ps1" file without the "running scripts is disabled" error.
    

As this may have its security implications, it's important to understand the risks associated with allowing script execution on your system.