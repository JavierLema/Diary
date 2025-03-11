---
attachments: [Clipboard_2024-11-05-09-29-02.png, Clipboard_2024-11-05-09-29-10.png, Clipboard_2024-11-05-09-46-55.png, Clipboard_2024-11-14-11-44-12.png]
tags: [React & NodeJS]
title: React and NodeJS
created: '2024-11-05T08:28:46.846Z'
modified: '2025-01-29T10:41:24.086Z'
---

# React and NodeJS
### Steps to work.
- Open ClientApp on VSCode and compile an run project.
- Open VStudio
  + Change the aspx page to load resources from local:
  ![](@attachment/Clipboard_2024-11-05-09-46-55.png)

  ```
    #if DEBUG
			RadScriptManager.Scripts.Add(new ScriptReference("http://localhost:8080/static/js/vendor.chunk.js"));
			RadScriptManager.Scripts.Add(new ScriptReference("http://localhost:8080/static/js/common.chunk.js"));
			RadScriptManager.Scripts.Add(new ScriptReference("http://localhost:8080/static/js/pages/mylibrary.js"));
    #else
			TelerikUtils.AddVersionedScript(RadScriptManager, "/ClientApp/build/static/js/vendor.chunk.js");
			TelerikUtils.AddVersionedScript(RadScriptManager, "/ClientApp/build/static/js/common.chunk.js");
			TelerikUtils.AddVersionedScript(RadScriptManager, "/ClientApp/build/static/js/pages/mylibrary.js");
    #endif
  ```


  + Run RFEWeb project.


### Possible errors:
- ![](@attachment/Clipboard_2024-11-14-11-44-12.png)  It's possible to load a different js in aspx page?
  


