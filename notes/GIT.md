---
tags: [HowTo, TIPS]
title: GIT
created: '2024-11-05T10:03:42.217Z'
modified: '2024-11-25T11:06:25.506Z'
---

# GIT
### To add a remote respository without download all code:
- Add a remote repository ```git remote add glawccc https://github.com/glawccc/rightfind-enterprise.git```
- Fetch all changes ```git fetch glawccc```
- Checkout any remote branch ```git checkout glawccc/master```
- Switch to remote branch ```git switch -c glawccc_14470 glawccc/RFE-14470-AddToAnotherLib```

### Push a local branch in remote repository:
- ```git push --set-upstream origin RFE-17584_Branch```

### Show all remote branches
- ```git remote -r -v```

### Show all remote repositories configured.
- ```git remote -v```

### Show branches for a remote repository
- ```git remote show glawccc```





