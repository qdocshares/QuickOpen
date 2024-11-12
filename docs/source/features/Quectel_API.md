# Quectel APIs



## device management

ql_mcm_dm.h

| Functions | Description |
| ------    | ------      |
| QL_MCM_DM_Client_Init()  |  Initializes device management service.  |
| QL_MCM_DM_AddRxIndMsgHandler()  | Sets the callback function triggered after the airplane 
mode is changed into another mode. |
| QL_MCM_DM_SetAirplaneModeChgInd()  | Sets the switch to trigger the execution of callback 
function after the airplane mode changes. |
| QL_MCM_DM_GetAirplaneMode()  | Gets airplane mode of the module | 
| QL_MCM_DM_SetAirplaneMode()  | Sets airplane mode of the module.|
| QL_MCM_DM_Client_Deinit() | De-initializes device management service. |
| QL_MCM_DM_GetSerialNumbers()  | Gets the IMEI and MEID information of the module. |
| QL_MCM_DM_GetFirmware()  | Gets the firmware version information of the module. |


## SMS

ql_mcm_sms.h

| Functions | Description |
| ------    | ------      |
| QL_SMS_Client_Init()   | Initializes SMS to obtain the handle.  |
| QL_SMS_Client_Deinit() | Deregisters SMS. |
| QL_SMS_GetSmsCenterAddress() | Gets the SMS center number and type. |
| QL_SMS_SetSmsCenterAddress() | Sets the SMS center number and type. |
| QL_SMS_Send_Sms()         | Sends a text message. |
| QL_SMS_AddRxMsgHandler()  | Sets the callback function for text message receiving. |
| QL_SMS_Send_SmsPdu()      | Sends an SMS message in PDU mode. |


## GPS

ql_mcm_gps.h


| Functions | Description |
| ------    | ------      |
| QL_LOC_Client_Init  |Initialize a GNSS client  |
| QL_LOC_Client_Deinit | Deregister a GNSS client | 
| QL_LOC_AddRxIndMsgHandler | Register a callback function to process GNSS data |
| QL_LOC_Set_Indications | Set indications of callback data |
| QL_LOC_Start_Navigation | Start GNSS |
| QL_LOC_Stop_Navigation | Stop GNSS |
| QL_LOC_Set_Position_Mode | Set position configuration items |
| QL_LOC_Get_Current_Location | Get current location data |
| QL_LOC_Delete_Aiding_Data | Delete GNSS auxiliary data |
| QL_LOC_InjectTime | Inject UTC time to GNSS |
| QL_LOC_InjectLocation  | Inject location data to GNSS |
| QL_LOC_Xtra_InjectData | Inject XTRA auxiliary data to GNSS |
| QL_LOC_Xtra_InjectFile  | Inject XTRA file to GNSS |
| QL_LOC_Agps_DataConnOpen  | Notify that AGPS data connection is opened  |
| QL_LOC_Agps_DataConnClose | Notify that AGPS data connection is closed  |
| QL_LOC_Agps_NfyDataConnFailed | Notify the failure of starting a AGPS data connection |
| QL_LOC_Agps_SetServer | Set AGPS server address and port |
| QL_LOC_NI_SetResponse  | Send NI user responses  |
| QL_LOC_Agps_UpdateNWAvailability | Update network availability |


## 



