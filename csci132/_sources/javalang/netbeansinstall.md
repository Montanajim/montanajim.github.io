# NetBeans Installation

## Three Main Steps

1. Install Open JDK

2. Set the Environmental Variables in Windows

3. Install Apache NetBeans. 

   

   For fresh installs, it has to be done in this order.

## Install Open JDK

1. Go to https://openjdk.java.net/Click on the version you wish to install.<img src="https://lh5.googleusercontent.com/03cmca3Fv8gRQt_9b4KGmNSO8uttXaeD4K57S5jQ0MSe2TKNS9NVP6twbk4_gMp7eoDY2-ByRkvGPiov6BfWqbRZMqCGAQvQV4bnSInns7PrFrmX21_ZUKejHtiGE-kdnTWvyfdC9fBPr22kbA" alt="img" style="zoom:75%;" />

   2. *Uncompress the zip or gz file*. For Windows, copy the java-xx file to c:\\Program Files in a folder called java. **C:\Program Files\Java\java-xx**. 

   

   ## Set the Environmental Variables in Windows

   1. Depress the Windows Key and release then type ENV. This will open the window to change the environmental variables.

   2. ![img](https://lh5.googleusercontent.com/0bjY3gjaNvmxhg74qtGmRbfVDRKwKzAzdop0G3_R2Jt1VFLELBwYGKt5TifNS_vAmTkxLbxfXnl2wShrrgMpSdTtrkOHCqbCREwX5XuPf_uHRGhpkVodI2IwGV2jbIxf14kCpSUc8x2ujV1cgw)

   3. Set a PATH: Select Control Panel and then System.

      1. Click Advanced and then Environment Variables.
      2. Add the location of the **bin folder** of the JDK installation to the PATH variable in System Variables.
      3. Click **Path** in the System Variables (bottom half), click **edit**, and **browse**. Browse to the **bin** folder and click **ok**."C:\Program Files\Java\jdk-xx\bin"

   4. Set JAVA_HOME:

      1. Under System Variables, click New.

      2. Enter the variable name as **JAVA_HOME**. 

		:::{warning}
		JAVA_HOME has to be in all caps.
		:::

      3. Enter the variable value as the installation path of the JDK (without the bin sub-folder)
      4. Click OK.
      5. Click OK.

## Install Apache NetBeans

1. Go to https://netbeans.apache.org/
2. Click the download button.
3. Install


Updated May 2022