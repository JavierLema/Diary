---
tags: [TIPS]
title: Development
created: '2025-02-19T08:27:24.826Z'
modified: '2025-02-19T08:53:24.018Z'
---

# Development

<details>
  <summary>Flags and Enums</summary>
    
    ***How to show the value of int value when used flags?***
    
    ImportApprovalStatuses[] statuses = (ImportApprovalStatuses[])Enum.GetValues(typeof(ImportApprovalStatuses));
    foreach (ImportApprovalStatuses stat in statuses)
    {
        Debug.WriteLine($"{stat} => {(int)stat}");
    }

    var flag_1 = (ImportApprovalStatuses)262144;
    var flag_3 = (ImportApprovalStatuses)139264;
    var flag_2 = (ImportApprovalStatuses)401408;
    foreach (ImportApprovalStatuses stat in statuses)
    {

        if (flag_1.HasFlag(stat))
        Debug.WriteLine($"Flag1 contains {(int)stat}");

        if (flag_2.HasFlag(stat))
        Debug.WriteLine($"Flag2 contains {(int)stat}");
    }
</details>
