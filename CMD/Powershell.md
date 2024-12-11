---
lastSync: Wed Dec 11 2024 04:28:23 GMT+0000 (Greenwich Mean Time)
---
**Modify the timestamp property of a file**
1. open [[Powershell with admin access
2. type in: `(Get-Item "C:\Users\file.pdf").CreationTime=("1 December 2004 17:00:00")`
3. `CreationTime`, `LastWriteTime`, `LastAccessTime`