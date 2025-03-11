---
attachments: [Clipboard_2025-01-31-11-25-17.png]
tags: [_Refinement]
title: Weekly Refinement Sessions -
created: '2024-11-29T09:35:26.336Z'
modified: '2025-03-07T08:48:59.979Z'
---

# Weekly Refinement Sessions -

<details>
  <summary>Tuesday/Wednesday - March 11th/12th, 2025</summary>

  + RFE-18277: [SPIKE][TECH] Connect a Lambda with the RFE database by Valentina Imaicheva to make final decisions related to implementation. 
  + GOAL 1 – ET-193: Sovos Integration: Support notifications – 2 stories
    - RFE-18289: [TECH] New notification endpoint service
    - RFE-19539: [TECH] Lambda notification system - Successful import
  + GOAL 3 – ET-147: AI Licensing – 1 story
    - RFE-19684: [RFE+AM] AI Licensing - CUO/RS page: Show AI rights granted when it is configured as granted in the source.
  + GOAL 4 - ET-169: SHARED LIBRARIES – pre-UAT/UAT – 8 stories – PI26
    - RFE-19517: [Pre-UAT] Add Tags: Adjust the Search bar's size with the end of the "Available Tags" section.
    - RFE-19516: [Pre-UAT] Library main page: (Un)Check a row by clicking anywhere in the cell.
    - RFE-19598: [Pre-UAT] Library menu: Indent Libraries under the Shared Libraries option.
    - RFE-18682: [Pre-UAT] Filters tab: Rename 2 filter options
    - RFE-19561: [Pre-UAT] Citations contextual menu: Get rid the "Open" option
    - RFE-19558: [Pre-UAT] Library name: Hide library's title tooltip when focus changes
    - RFE-19601: [Pre-UAT] Citation's contextual menu: New option to configure Custom field values
    - RFE-19562: [Pre-UAT] Read/Unread: Show a tooltip to explain the meaning of the icon
  + GOAL 5 - Prepare Technical backlog - X stories

</details>

<details>
  <summary>Tuesday/Wednesday - February 25th/26th, 2025</summary>

    + GOAL 1 – ET-147 -AI Licensing – 1 story - EPIC FINISHED!
      - RFE-19684: [RFE+AM] AI Licensing - CUO/RS page: Show AI rights granted when it is configured as granted in the source.
    + GOAL 2 – ET-185 – [TECH] Resource Center - Redirection Authentication - 1 story- EPIC FINISHED!
      - RFE-19652: [TECH] RFE Authentication redirect to RC
    GOAL 3 - ET-157: Integrate with Sovos Tax rate table feed – 6 stories
    
    RFE-18274: [TECH] Create a Model and a repository for the SalesTax table.
    RFE-18273: [TECH] Modify the CalcTaxHelper Function.
    RFE-18278: [TECH] Create a script to Populate SalesTax Table.
    RFE-19537: [TECH] Lambda process creation with logic and CI/CE support. ->Pending of finishing the spike.
    RFE-19542: [TECH] Lambda schedule request and follow-up.
    RFE-19543: [TECH] Lambda process - Include reattempt's logic.
    GOAL 4 – ET-171 – CAS – Hybrid CAS integration – 4 stories
    RFE-19429: [TECH] Fix compatibility with security fixes.  
    RFE-19430: [SPIKE] Investigate how to authenticate users that are in PRM but not in RFE.
    RFE-19433: [SPIKE] Investigate how to map CAS tickets to RFE session IDs.
    RFE-19220: [SPIKE] Investigate plans of integration with RFE.
    GOAL 5 – ET-189 – CAS – Support sign-in via CAS via SAML – 2 stories
    RFE-19673: [SPIKE] Investigate how to store PRM organization IDs in RFE for clients
    RFE-19671: [SPIKE] Investigate how to retrieve SAML assertions from CAS or PRM.
    GOAL 6 – ET-172 – [SPIKE] Findout search features to improve NAV/RFE search - 1 story EPIC FINISHED!
    RFE-18517: [SPIKE] Findout how to include Exact match in search for improving cross-Nav.
    GOAL 7: Prepare Technical backlog - 4 stories
    RFE-19919: [Tech] Get rid of TagActionsDropdown to avoid confusions for developers and use a better component
    RFE-19917: [Tech] Get rid of TagsList and AddTagListItem to avoid confusions for developers and use a better component
    RFE-19987: [Tech] Fix SonarQube errors in React
    RFE-19993: [SPIKE] Document how our matching algorythm work currently

</details>

<details>
  <summary>Tuesday/Wednesday - February 18th/19th, 2025</summary>

    GOAL 1 – ET-147 - AI Licensing – 2 stories
    RFE-15700: [RFE+AM] AI Licensing - Show the AI right with its configurable options at Collection's level
    RFE-15915: [RFE+AM] AI Licensing - Show the AI right with its configurable options at Holding's level
    GOAL 2 - ET-175 – [TECH] Prepare report templates based on GA data - 2 stories
    RFE-19288:[TECH] Extend GA logging for "Global-search" component to log raw search data.
    RFE-19288: [TECH] Prepare report templates based on GA data
    GOAL 3 – ET-161 - [SPIKE] RFE API - Retrieve Esourcing template information to facilitate the PDF Direct fulfillment – 1 story
    RFE-19189: [TECH] New endpoint to get standard esources templates
    GOAL 4: Prepare Technical backlog - X stories
    [TBD] Pending to be provided by Juan Zurita Bobis / Ivan Sterkhov
 
</details>


<details>
  <summary>Tuesday/Wednesday - February 4th/5th, 2025</summary>

  - GOAL 1 - ET-178 – Tagging - Control the character entry in import processes to only supported characters - 1 story
    + RFE-19299: CRO page: Tags creation to be aligned with SL/Doc. Viewer.
      
  - GOAL 2 - ET-161 – Spikes/Implementation to facilitate the PDF direct fulfillment in the Suite - 3 stories
    + RFE-18411: [SPIKE] Collect information related to Standard ESources templates and macros
      **RFE Affected Section** Application Configuration → Standard ESources

    ![](@attachment/Clipboard_2025-01-31-11-25-17.png)

    + RFE-19187: [SPIKE] Information related to proxies
      **RFE Affected Section** Client Management → Proxy Servers

    + RFE-19190: [SPIKE] Collect information related to Standard ESources attempt errors provided by RFE API REST
      **RFE Affected Section** Application Configuration → Standard ESources

  - GOAL 3 – ET-170 -[SPIKE] Shared Libraries - Add Next gen libraries as a second library option
    + RFE-18671: Review CAS integration’s spike
      - **Party Management UI** https://prm-mgmt-ui.aws-p-dev.copyright.com/

  - GOAL 4 – Top ten/Shared Library stories – Should have/Could have – 2 stories
    + RFE-13683: [PO09] Enable Manual online in fullfilment. Only if it is ready for QA team.
      **RFE Affected Section** Data Management → Collections

    + RFE-19175: Detail view is missing document type icons (document/IOI/linkout)
      The icon column dessapears on the new design.

  - GOAL 5: Prepare Technical backlog - 2 stories
    + RFE-19490: [Tech] Rework how we are working with toast messages in RFE
      http://styles.aws-del-prd.copyright.com/docs/patterns/inline-notifications -> Dima says: "It is a bit different thing"

    + RFE-13670: [Architecture] Investigate replacing current session in RFE with a cache based solution
 
</details>

<details>
  <summary>Tuesday/Wednesday - January 28/29th, 2025 – 90 min/session</summary>

  Hi Refinement! Following is the draft agenda for our next week sessions. Per usual, drop a comment if you have any other items you´d want to discuss:
  - GOAL 1: Shared Library adjustments with tags (ET-85/ET-95) – 4 stories – PI25
    + *RFE-14460*: SL-Filters tab - Include "Empty" option in selectable filter field
    + *RFE-18683*: Filters tab - Include "None" option in selectable filter field - API REST
    + *RFE-18682*: Filters tab - Include "None" option in selectable filter field - Other RFE areas
    + *RFE-18379*: Manage Tags - Ability to highlight an existing tag when we detect a duplication.
      
  - GOAL 2: Prepare Tagging – Entry to only supported characters (ET-120) - 1 story – PI25
    + *RFE-18794*: New Library IMPORT – Limit tags characters entry to only supported characters
    + **user experience = "lo peor"**
  - GOAL 3 – Additional stories raised during the PI24 – Could have – 3 stories - PI25
    + *RFE-18222*: Let the user to copy the linkout/DRM URL by using a new "Copy URL" option. 
    + *RFE-13683*: [PO09] Enable Manual online in fullfilment.
    + *RFE-18634*: Create feature toggle for Sorting by Parent Title.
  - GOAL 4: Prepare Technical backlog - X stories
    + *RFE-18534*: [TECH] Merge Performance Logging changes for Order Processor

  TOTAL: 8 stories + 1 technical story

  **NOTE**: In case we'd finish all the tickets on Tuesday we could use the Wednesday session slot to review the CAS's spike if Erik Krebs would be available. Yaroslav Morozov / Juan Zurita Bobis
  **NOTE**: Team’s preparation day will be on Friday, 23th of January.  Thanks!
  
</details>



