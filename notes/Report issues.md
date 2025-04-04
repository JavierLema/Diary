---
attachments: [Clipboard_2025-03-14-13-49-54.png, Clipboard_2025-03-14-13-50-04.png, Clipboard_2025-03-14-13-50-50.png, Clipboard_2025-03-14-13-51-37.png, Clipboard_2025-03-25-12-22-47.png, Clipboard_2025-03-25-12-22-57.png, Clipboard_2025-03-27-13-20-44.png]
tags: [__JIRA Tickets]
title: Report issues
created: '2025-03-14T12:48:38.662Z'
modified: '2025-04-03T10:14:07.820Z'
---

# Report issues

<details>
  <summary>Resolution</summary>

  Change all wrong reports in all environments by TTS.
  This is the path to locate these reports.
  - DEV:  \\win-rfe-dev\rfedev\data\_reportTemplates 
  - TEST: \\win-rfe-test.copyright.com\rfetest\data_reportTemplates
  - PS:   \\win-rfe-ps.copyright.com\rfeps\data\_reportTemplates
  - PRD:  \\win-rfe-prd.copyright.com\rfeprd\data_reportTemplates

</details>

<details>
  <summary>VIM</summary>

  To identify one character in Vim editor, use ga.

  ![](@attachment/Clipboard_2025-03-27-13-20-44.png)

  ![](@attachment/Clipboard_2025-03-25-12-22-47.png)
  ![](@attachment/Clipboard_2025-03-25-12-22-57.png)
</details>

<details>
  <summary>Report history - Check invalid characters.</summary>

  - 9fcc2bb2078e495884c14bfc2a128818b596fba2 --> Author: glaw <glaw@copyright.com>  2016-01-12 16:49:08
  - **LAST UPDATE** 43619e7c55c39e6488152f623dd5687687098ce8 --> Author: victor-sharovatov <victor_sharovatov@epam.com>  2018-04-17 16:23:05

  ```
  public static void AnalizeReports()
  {
      StringBuilder sb = new StringBuilder();

      DirectoryInfo di = new DirectoryInfo(@"C:\Temp\Reports\43619e7c55c39e6488152f623dd5687687098ce8");
      //DirectoryInfo di = new DirectoryInfo(@"C:\Temp\Reports\05b08cda1fa18feb5b77052652d27fa96a34fd7b");
      foreach (var fi in di.GetFiles("*.rdl"))
      {
          using (StreamReader reader = new StreamReader(fi.FullName))
          {
              var content = reader.ReadToEnd();
              try
              {
                  XDocument doc = XDocument.Parse(content);
                  string validXML = XmlConvert.VerifyXmlChars(content);

                  var invalidChars = (from chr in content
                                      where ((int)chr) < 0 || ((int)chr) > 255
                                      select chr).ToList();

                  if (invalidChars.Any())
                  {
                      sb.AppendLine($"Report: {fi.Name} Is NOT valid [{string.Join(" ", invalidChars.ToArray())}]");
                      foreach(Char c in invalidChars.Distinct())
                      {
                          Console.WriteLine($"{c} => {(int)c}");
                      }
                  }
              }
              catch(Exception ex)
              {
                  Debug.WriteLine($"Analize: {fi.Name} --> FALSE");
                  Debug.WriteLine(ex.Message);
              }
          }
      }
      var text = sb.ToString();
  }
  ```

</details>


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
