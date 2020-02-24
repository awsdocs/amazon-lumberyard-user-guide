# Setting Up PyCharm for Debugging Waf<a name="az-code-gen-pycharm"></a>


****  

|  | 
| --- |
| AZ Code Generator is in preview release and is subject to change\. | 

PyCharm is an integrated development environment for Python which includes a graphical debugger that is useful for debugging Waf\. 

**To set up PyCharm and Waf for debugging**

1. Download [PyCharm Community Edition](https://www.jetbrains.com/pycharm/download/)\. 

1. Start PyCharm\. 

1. At the welcome screen, choose **Open Directory**\.  

1. From the Lumberyard root directory, navigate to any branch that contains a `_WAF_` or `dev` directory\.  There should be a file called `wscript` and `waf_branch_spec.py` under this folder\. 

1. Configure the Python interpreter\. 

   1. Choose **File**, **Settings**, **Project:dev**, **Project Interpreter** to open the project interpreter page\. 

   1. Click the gear ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/cloud-canvas-cloud-gem-text-to-speech-cgp-4.png) icon on the right of the **Project Interpreter** and choose **Add Local**\.   
![\[Add Local\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-1.png)

   1. Navigate to the folder where `python.exe` resides\.  The Python executable file must be in the same folder as the project or you may have issues running Waf\.   
![\[Verify the location of python.exe\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-2.png)

1. Set up a debugging profile for Waf\. 

   1. To set up Waf for debugging, use the project explorer in the left pane\.  If you don't see the project explorer, press **Alt\+1**\)\.  Navigate to the `\dev\Tools\Build\waf-<version>` node and expand it\. You should see a file called `lmbr_waf` inside this node\.   
![\[The lmbr_waf file\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-3.png)

   1. Right\-click **lmbr\_waf** and choose **Create lmbr\_waf** 
**Note**  
The **Indexing\.\.\.** operation must finish before the option appears\. You can verify status in the bar at the bottom\.   
![\[Create lmbr_waf\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-4.png)

   1. In the **Create Run/Debug Configuration** dialog, ensure that the following values are configured correctly:
      + **Single instance only** should be selected\. 
      + **Script Parameters** is the command to use to run Waf for the run/debug session\. 
      + **Python Interpreter** should be the interpreter that you specified earlier\. 
      + The **Working directory** must be the root of the project \(for example, the `dev` directory\)\.   
![\[Configure debugging\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-5.png)

      Next, you must to set up `wscript` files as debuggable Python files\. Waf uses files called `wscript` to define the build rules per project\.  These are dynamically loaded Python modules that can be debugged like any other Python module\.  

   1. Choose **File**, **Settings**, **Editor**, **File Types**, **Python**\. 

   1. To add a registered pattern for **wscript**, choose **Python** in **Recognized File Types**\.   
![\[Choose Python\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-6.png)

   1. Under **Registered Patterns**, click the green plus sign \(**\+**\)\. 

   1. In the **Add Wildcard** dialog box, enter **wscript**\.   
![\[Add wscript wildcard\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-7.png)

1. Make sure **IncrediBuild** is turned off\. 

   1. Open the `_WAF_/usersettings.options` file\.

   1. Verify that `use_incredibuild` is set to false, as in the following example\. `use_incredibuild = False` 

1. \(Optional\) Enable file outlining\.

   By default, file outlining is switched off in PyCharm\. This feature facilitates navigation in the source files, as the following image shows\.  
![\[File outlining\]](http://docs.aws.amazon.com/lumberyard/latest/userguide/images/az-code-gen-pycharm-8.png)

   To enable file outlining, right\-click the **Project** tab and choose **Show Members**\. 