---
tags: [TIPS]
title: RFE common TIPS
created: '2022-08-18T08:25:46.921Z'
modified: '2025-01-24T12:02:28.633Z'
---

# RFE common TIPS

<details>
  <summary>Other applications tips</summary>
  
  * FYI: **Jira accept a case sensitive labels**, but when you search for them, the **search results are case insensitive**.
</details>

- To view Log file you need:
    * Configure vl/vlib/serilog.config with these values:
        - `<add key="messages:serilog:minimum-level" value="Error" />` **Error/Verbose/...**
        - `<add key="messages:serilog:write-to:File.path" value="C:\Logs\rfeWeb_Message..log" />`

    * Use a linux tail command:
        - For example: tail -f /c/Logs/rfeWeb_Message.20221128.log



Search control poc
