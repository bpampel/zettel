---
title: Git search repository
date: 2021-07-14 12:37
---
Remember implementing some feature but can't find it?
Was it changed later? Is it in some unmerged branch?

For small (**!**) repositories you can grep through all commits:

```git rev-list --all | xargs git grep "my search"```

