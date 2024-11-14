# ACDB

ACDB (Audio Calibration Database)

ACDB is used to adjust ADSP audio parameters. As shown in the figure below, there are currently 7 ACDB 
files available for use. The workspaceFile.qwsp shown below is a project file for the QACT tool to open the
ACDB files. 

QACT, a kind of audio parameters adjustment tool provided by Qualcomm, is used to calibrate ACDB.
ACDB files are loaded into memory in the process of alsaucm_test. If the process is not enabled, online 
calibration mode cannot be used on QACT tool.

## import ACDB

Copy the SDK to Linux and execute the following command to unzip the SDK.

    unzip sudo tar -jxvf EC20CETFDKR05A03V01M2G_OCPU_DJJ_SDK.tar.bz2



