---
attachments: [Clipboard_2025-03-14-13-49-54.png, Clipboard_2025-03-14-13-50-04.png, Clipboard_2025-03-14-13-50-50.png, Clipboard_2025-03-14-13-51-37.png]
tags: [__JIRA Tickets]
title: Report issues
created: '2025-03-14T12:48:38.662Z'
modified: '2025-03-14T13:37:40.304Z'
---

# Report issues

<details>
  <summary>RFE-20330</summary>

  ### Order History Report not exporting Japanese characters when Default Cuture set to Japanese
  The error 

  ![](@attachment/Clipboard_2025-03-14-13-49-54.png)

  ![](@attachment/Clipboard_2025-03-14-13-50-04.png)

  ![](@attachment/Clipboard_2025-03-14-13-50-50.png)

  ![](@attachment/Clipboard_2025-03-14-13-51-37.png)

  #### Search results from Diff using VIM with this regular expresion "[^\x00-\xFF]" ascii extended 

  - vl/VLReports/30 UCB Other Invoice.rdl
    + <Value>Infotrieve GmbH, Beethovenstr. 8, **DпїЅ**50674 Cologne</Value>
  - vl/VLReports/30 UCB Germany Invoice.rdl
    + <Value>Information Retrieval GmbH
        +Beethovenstr. 8
        +**DпїЅ**50674 Cologne
        +www.infotrieve.com
      </Value>
  - vl/VLReports/CB-CR GMY-TO_US.rdl
    +  <Format>**пїЅ**#,#.##</Format>
  - vl/VLReports/CB-FF US-TO-GMY.rdl
    +  <Format>**пїЅ**#,#.##</Format>	
  - vl/VLReports/ISI Class I.rd
    + <Value>Monthly Reporting **пїЅ** Revenue/Servicing Fees</Value>
  - vl/VLReports/ISI Class IV.rdl
    + <Value>Monthly Reporting **пїЅ** Revenue/Servicing Fees</Value>
  - vl/VLReports/MyRequests.rdl
    + Status traductions

</details>
