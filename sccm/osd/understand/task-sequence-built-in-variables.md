---
title: Task sequence built-in variables
titleSuffix: "Configuration Manager"
description: "Task sequence built-in variables provide information about the environment where the task sequence runs and are available during the whole task sequence."
ms.custom: na
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02bc6bd4-ca53-4e22-8b80-d8ee5fe72567
caps.latest.revision: 15
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: dougeby

---
# Task sequence built-in variables in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


 Task sequence built-in variables are provided by System Center Configuration Manager. Built-in variables provide information about the environment where the task sequence is running, and their values are available throughout the whole task sequence. Typically, built-in variables are initialized before steps are run in the task sequence. For example, the built-in variable **_SMSTSLogPath** is an environment variable that specifies the path that Configuration Manager components use to write log files. Any task sequence step can access this environment variable. However, the task sequence evaluates some variables, such as **&#95;SMSTSCurrentActionName**, before each step. The values are read only for built-in variables with a name that begins with an underscore.  

## Task Sequence Built-in Variable List  
 The following list describes the built-in variables that are available in Configuration Manager:  

|Built-in Variable Name|Description|  
|-----------------------------|-----------------|  
|_OSDDetectedWinDir|The task sequence scans the computer's hard drives for a previous operating system installation when Windows PE starts. The Windows folder location is stored in this variable. You can configure your task sequence to retrieve this value from the environment and use it to specify the same Windows folder location to use for the new operating system installation.|  
|_OSDDetectedWinDrive|The task sequence scans the computer's hard drives for a previous operating system installation when Windows PE starts. The hard drive location for where the operating system is installed is stored in this variable. You can configure your task sequence to retrieve this value from the environment and use it to specify the same hard drive location to use for the new operating system.|  
|_SMSTSAdvertID|Stores the current running task sequence deployment unique ID. It uses the same format as a Configuration Manager software distribution deployment ID. If the task sequence is running from stand-alone media, this variable is undefined.<br /><br /> Example:<br /><br /> **ABC20001**|  
|_TSAppInstallStatus|The task sequence sets the _TSAppInstallStatus variable with the installation status for the application during the [Install Application](task-sequence-steps.md#BKMK_InstallApplication) step. The task sequence sets the variable with one of the following values:<br /><br /> 1. **Undefined**: The Install Application step has not run.<br />2. **Error**: At least one application failed because of an error during the Install Application step.<br />3. **Warning**: No errors occur during the Install Application step. One or more applications, or a required dependency, did not install because a requirement was not met.<br />4. **Success**: There are no errors or warnings detected during the Install Application step.|  
|_SMSTSBootImageID|If the current running task sequence references a boot image package, this variable stores the boot image package ID. If the task sequence does not reference a boot image package, this variable is not set.<br /><br /> Example:<br /><br /> **ABC00001**|  
|_SMSTSBootUEFI|The task sequence sets the SMSTSBootUEFI variable when it detects a computer that is in UEFI mode.|  
|_SMSTSClientGUID|Stores the value of Configuration Manager client GUID. This variable is not set if the task sequence is running from stand-alone media.<br /><br /> Example:<br /><br /> **0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c**|  
|_SMSTSCurrentActionName|Specifies the name of the currently running task sequence step. This variable is set before the task sequence manager runs each individual step.<br /><br /> Example:<br /><br /> **run command line**|  
|_SMSTSDownloadOnDemand|If the current task sequence is running in download-on-demand mode, this variable is **true**. Download-on-demand mode means the task sequence manager downloads content locally only when it must access the content.|  
|_SMSTSInWinPE|When the current task sequence step is running in Windows PE, this variable is **true**. Test this task sequence variable to determine the current operating system environment.|  
|_SMSTSLastActionRetCode|Stores the return code that was returned by the last action that was run. This variable can be used as a condition to determine if the next step is run.<br /><br /> Example:<br /><br /> **0**|  
|_SMSTSLastActionSucceeded|If the last step succeeded, this variable is **true**. If the last step failed, it is **false**. If the task sequence skipped the last action, because the step is disabled or the associated condition evaluated to **false**, this variable is not reset. It still holds the value for the previous action.|  
|_SMSTSLaunchMode|Specifies one of the following task sequence launch methods:<br /><br /> -   **SMS**: the task sequence started from the Configuration Manager client<br />-   **UFD**: the task sequence started from legacy USB media<br />-   **UFD+FORMAT**: the task sequence started from newer USB media<br />-   **CD**: the task sequence started from a CD<br />-   **DVD**: the task sequence started from a DVD<br />-   **PXE**: the task sequence started from PXE<br />-   **HD**: the task sequence started from prestaged media on a hard disk|  
|_SMSTSLogPath|Stores the full path of the log directory. Use this value to determine where actions are logged. This value is not set when a hard drive is not available.|  
|_SMSTSMachineName|Stores and specifies the computer name. Stores the name of the computer that the task sequence uses to log all status messages. To change the computer name in the new operating system, use the **OSDComputerName** variable.<br /><br /> Example:<br /><br /> **ABC**|  
|_SMSTSMDataPath|Specifies the path defined by the SMSTSLocalDataDrive variable. When you define SMSTSLocalDataDrive before the task sequence starts, such as by setting a collection variable, Configuration Manager then defines the _SMSTSMDataPath variable once the Task Sequence starts.|  
|_SMSTSMediaType|Specifies the type of media that is used to initiate the installation. Examples of types of media are Boot Media, Full Media, PXE, and Prestaged Media.|  
|_SMSTSMP|Stores the URL or IP address of a Configuration Manager management point.|  
|_SMSTSMPPort|Stores the management point port number of a Configuration Manager management point.<br /><br /> Example:<br /><br /> **80**|  
|_SMSTSOrgName|Stores the branding title name that the task sequence displays in the progress dialog.<br /><br /> Example:<br /><br /> **XYZ Organization**|  
|_SMSTSOSUpgradeActionReturnCode|Stores the exit code value that Windows Setup returns to indicate success or failure. This variable is set during the [Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS) task sequence step. This variable is useful with the /Compat command-line option.<br /><br /> Example:<br /><br /> On the completion of /Compat, take action in later steps depending on the failure or success exit code. On success, initiate the upgrade. Or, set a marker in the environment (for example, add a file or set a registry key) to collect with hardware inventory. Use this marker to create a collection of computers that are ready to upgrade, or that require action before upgrade.|  
|_SMSTSPackageID|Stores the current running task sequence ID. This ID uses the same format as a Configuration Manager software package ID.<br /><br /> Example:<br /><br /> **HJT00001**|  
|_SMSTSPackageName|Stores the current running task sequence name specified by the Configuration Manager administrator when the task sequence is created.<br /><br /> Example:<br /><br /> **Deploy Windows 10 task sequence**|  
|_SMSTSSetupRollback|Specifies whether the operating system Setup performed a rollback operation. The variable values can be **true** or **false**.|  
|_SMSTSRunFromDP|Set to **true** if the current task sequence is running in run-from-distribution-point mode, which means the task sequence manager obtains required package shares from distribution point.|  
|_SMSTSSiteCode|Stores the site code of the Configuration Manager site.<br /><br /> Example:<br /><br /> **ABC**|  
|_SMSTSType|Specifies the type of the current running task sequence. It can have the following values:<br /><br /> **1** - indicates a generic task sequence.<br /><br /> **2** - indicates an operating system deployment task sequence.|  
|_SMSTSTimezone|The _SMSTSTimezone variable stores the time zone information in the following format (without spaces):<br /><br /> Bias, StandardBias, DaylightBias, StandardDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, DaylightDate.wYear, wMonth, wDayOfWeek, wDay, wHour, wMinute, wSecond, wMilliseconds, StandardName, DaylightName<br /><br /> Example:<br /><br /> For the Eastern Time U.S. and Canada, the value would be **300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time**|  
|_SMSTSUseCRL|When the task sequence uses HTTPS to communicate with the management point, specifies whether it uses the certificate revocation list (CRL).|  
|_SMSTSUserStarted|Specifies whether a task sequence is started by a user. This variable is set only if the task sequence is started from the Software Center. For example, if **_SMSTSLaunchMode** is set to **SMS**. The variable can have the following values:<br /><br /> -   **true** - specifies that the task sequence is manually started by a user from the Software Center.<br />-   **false** - specifies that the task sequence is initiated automatically by the Configuration Manager scheduler.|  
|_SMSTSUseSSL|Specifies whether the task sequence uses SSL to communicate with the Configuration Manager management point. If your site is running in native mode, the value is set to **true**.|  
|_SMSTSWTG|Specifies if the computer is running as a Windows To Go device.|  
|OSDPreserveDriveLetter|This task sequence variable is deprecated. During an operating system deployment, by default, Windows Setup determines the best drive letter to use (typically C:). <br /><br />Previous behavior: when applying an image, the OSDPreverveDriveLetter variable determines whether or not the task sequence uses the drive letter captured in the image file (.WIM). Set the value for this variable to **False** to use the location that you specify for the **Destination** setting in the **Apply Operating System** task sequence step. For more information, see [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|SMSTSAssignmentsDownloadInterval|The number of seconds to wait before the client attempts to download the policy since the last attempt that returned no policies. By default, the client waits **0** seconds before retrying.<br /><br /> You can set this variable by using a prestart command from media or PXE.|  
|SMSTSAssignmentsDownloadRetry|The number of times a client will attempt to download the policy after no policies are found on the first attempt. By default, the client retries **0** times.<br /><br /> You can set this variable by using a prestart command from media or PXE.|  
|SMSTSAssignUsersMode|Specifies how a task sequence associates users with the destination computer. Set the variable to one of the following values:<br /><br /> -   **Auto**: The task sequence creates a relationship between the specified users and destination computer when it deploys the operating system to the destination computer.<br />-   **Pending**: The task sequence creates a relationship between the specified users and the destination computer. An administrator must approve the relationship to set it.<br />-   **Disabled**: The task sequence does not associate users with the destination computer when it deploys the operating system.|  
|SMSTSDownloadAbortCode|This variable contains the abort code value for the external program downloader (specified in the SMSTSDownloadProgram variable). If the program returns an error code equal to the value of the SMSTSDownloadAbortCode variable, then the content download fails and no other download method is attempted.
|SMSTSDownloadProgram|Use this variable to specify an Alternate Content Provider, a downloader program that is used to download content instead of the default Configuration Manager downloader, for the task sequence. As part of the content download process, the task sequence checks the variable for a specified downloader program. If specified, the task sequence runs the program to perform the download.|  
|SMSTSDownloadRetryCount|The number of times that Configuration Manager attempts to download content from a distribution point. By default, the client retries **2** times.|  
|SMSTSDownloadRetryDelay|The number of seconds that Configuration Manager waits before it retries to download content from a distribution point. By default, the client waits **15** seconds before retrying.|
|SMSTSDriverReceiveTimeOut|The number of seconds before the connection to the server times out.|
|SMSTSErrorDialogTimeout|When an error occurs in a task sequence, it displays a dialog box with the error. The task sequence automatically dismisses it after the number of seconds specified by this variable. By default, this value is **900** seconds (15 minutes).|  
| TSDisableProgressUI | <!-- 1354291 --> Beginning in Configuration Manager version 1706, use this variable to control when the task sequence displays progress to end users. To hide or display progress at different times, set this variable multiple times in a task sequence. To hide task sequence progress, set the value of this variable to **True**. To display task sequence progress, set the value of this variable to **False**. | 
|SMSTSLanguageFolder|Use this variable to change the display language of a language neutral boot image.|  
|SMSTSLocalDataDrive|Specifies where temporary files are stored on the destination computer while the task sequence is running.<br /><br /> This variable must be set before the task sequence starts, such as by setting a collection variable. Once the task sequence starts, Configuration Manager defines the _SMSTSMDataPath variable once the Task Sequence starts.|  
|SMSTSMP|Use this variable to specify the URL or IP address of the Configuration Manager management point.|  
|SMSTSPeerDownload|Use this variable to enable the client to use Windows PE Peer Cache.<br /><br /> Example:<br /><br /> SMSTSPeerDownload  = **TRUE** enables this functionality.|  
|SMSTSPeerRequestPort|A custom network port that Windows PE peer cache uses for the initial broadcast. The default port configured in client settings is 8004.|  
|SMSTSPersistContent|Use this variable to temporarily persist content in the task sequence cache.|  
|SMSTSPostAction|Specifies a command that is run after the task sequence completes. For example, you can use this variable to specify a script that enables write filters on embedded devices after the task sequence deploys an operating system to the device.|  
|SMSTSPreferredAdvertID|Forces the task sequence to run a specific targeted deployment on the destination computer. Set this variable through a prestart command from media or PXE. If this variable is set, the task sequence overrides any required deployments.|  
|SMSTSPreserveContent|This variable flags the content in the task sequence to be retained in the Configuration Manager client cache after the deployment. This variable is different from SMSTSPersistContent, which only preserves the content for the duration of the task sequence. SMSTSPersistContent uses the task sequence cache, SMSTSPreserveContent uses the Configuration Manager client cache.<br /><br /> Example:<br /><br /> SMSTSPreserveContent = **TRUE** enables this functionality.|  
|SMSTSRebootDelay|Specifies how many seconds to wait before the computer restarts. If this variable is zero (0), the task sequence manager does not display a notification dialog before reboot.<br /><br /> Examples:<br /><br /> **0**: do not display a notification<br /><br /> **60**: display a notification for one minute|  
|SMSTSRebootMessage|Specifies the message to display in the restart notification dialog. If this variable is not set, a default message appears.<br /><br /> Example:<br /><br /> **The task sequence is restarting this computer**.|  
|SMSTSRebootRequested|Indicates that a restart is requested after the current task sequence step is completed. If a restart is required, just set this variable to **true**, and the task sequence manager will restart the computer after this task sequence step. If the task sequence step requires a restart to complete the action, set this variable. After the computer restarts, the task sequence continues to run from the next task sequence step.|  
|SMSTSRetryRequested|Requests a retry after the current task sequence step is completed. If this task sequence variable is set, the **SMSTSRebootRequested** must also be set to **true**. After the computer is restarted, the task sequence manager will rerun the same task sequence step.|  
|SMSTSUDAUsers|Specifies the primary users of the destination computer by using the following format:<br /><br /> Example:<br /><br /> **domain\user1, domain\user2, domain\user3**<br /><br /> Separate multiple users by using a comma (,). For more information, see [Associate users with a destination computer](../get-started/associate-users-with-a-destination-computer.md).|  
 
