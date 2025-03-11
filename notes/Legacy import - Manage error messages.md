---
tags: [__JIRA Tickets]
title: Legacy import - Manage error messages
created: '2025-02-13T08:14:34.233Z'
modified: '2025-03-05T06:08:56.417Z'
---

# Legacy import - Manage error messages

### RFE-18953 - Adapt rejected message to provide more information to the user

- Local Branch: RFE-18953_LEGACY_IMPORT-Adapt_rejected_message_to_provide_more_information_to_the_user

- Ana's branch:
  - RFE-18794-LimitTagsCharacters

Check a new implementation, overall multiple invalid chars or same invalid char in multiple tags.

### RFE-20183 - Incorrect_reject_reason_for_tags_with_some_non-printable_characters

Expected Results: 

Invalid Tag (Tag contains non-printable character(s))

Actual Results:

Invalid Tag (Tag contains invalid character(s): <b> </b>)
