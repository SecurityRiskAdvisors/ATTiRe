# ATTiRe Structured Logging Format

ATTiRe is Attack Tool Timing and Reporting. This is a machine-readable JSON-formatted superset of useful attack simulation reporting data for content creation and enrichment in tracking tools like VECTR. Use of a structured log format eases the creation of reporting detail and categorization of red team activities.

## Existing Community Logging Formats
Commercial and open source red team operator tools use proprietary logging formats to record the results of adversary emulation and attack simulation. Normalization and translation of this log data can be challenging. We're working with some community projects like Invoke-atomicredteam to build pluggable loggers that capture data to ATTiRe.

## Current Support

### Log Ingestion
* VECTR (https://vectr.io)
### Log Export
* VECTR's (https://vectr.io) portable executable attack automation components log to the ATTiRe format out of the box.
* SRA Invoke-atomicredteam fork awaiting upstream merge

## Future Goals
* UBJSON support - https://json.nlohmann.me/features/binary_formats/ubjson/
  * For embedding binary data like videos and screenshots rather than BASE64-encoding

## ATTiRe Sample
```js
{
    "attire-version": "1.1",
    "execution-data": {
        "execution-command": "Invoke-AtomicTest T1218.010 -TestNames \"Regsvr32 remote COM scriptlet execution\",\"Regsvr32 local DLL execution\"",
        "execution-id": "3im2GxwX9VG8jzXLTDegLEKY8WfrA1IXL0VUwhlDYWs=",
        "execution-source": "Invoke-Atomicredteam",
        "execution-category": {
            "name": "Atomic Red Team",
            "abbreviation": "ART"
        },
        "target": {
            "host": "WINDEV2009EVAL",
            "ip": "192.168.204.129",
            "path": "PATH=C:\\Windows\\system32;C:\\Windows",
            "user": "User"
        },
        "time-generated": "2021-10-27T02:00:57.439Z"
    },
    "procedures": [
        {
            "procedure-name": "Regsvr32 remote COM scriptlet execution",
            "procedure-description": "Run an exe on user logon or system startup.  Upon execution, success messages will be displayed for the two scheduled tasks. To view\nthe tasks, open the Task Scheduler and look in the Active Tasks pane.",
            "procedure-id": {
                "type": "guid",
                "id": "c9d0c4ef-8a96-4794-a75b-3d3a5e6f2a36"
            },
            "mitre-technique-id": "T1218.010",
            "order": 1,
            "steps": [
                {
                    "command": "powershell.exe -File \"T1218010 - Regsvr32 remote COM scriptlet execution\"",
                    "executor": "POWERSHELL",
                    "order": 1,
                    "output": [
                        {
                            "content": "File C:\\Users\\User\\Desktop\\AEv1.0 - Administrator-10\\T1070001 - Delete System Logs Using Clear-EventLog.ps1 cannot be \r\nloaded. The file C:\\Users\\User\\Desktop\\AEv1.0 - Administrator-10\\T1070001 - Delete System Logs Using \r\nClear-EventLog.ps1 is not digitally signed. You cannot run this script on the current system. For more information \r\nabout running scripts and setting execution policy, see about_Execution_Policies at \r\nhttps:/go.microsoft.com/fwlink/?LinkID=135170.\r\n    + CategoryInfo          : SecurityError: (:) [], ParentContainsErrorRecordException\r\n    + FullyQualifiedErrorId : UnauthorizedAccess",
                            "level": "STDERR",
                            "type": "console"
                        }
                    ],
                    "time-start": "2021-10-27T02:02:23.000Z",
                    "time-stop": "2021-10-27T02:02:25.000Z"
                }
            ]
        }
    ]
}
```
