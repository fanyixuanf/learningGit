## dev2
- ``` git checkout -b dev2 origin/main ```
- 我从错误的分支拉取了内容，或把内容拉取到了错误的分支
  - ``` git pull origin dev ```
    - ``` git reflog ```
      - ``` 6be641e (HEAD -> dev2, origin/dev2) HEAD@{0}: checkout: moving from dev to dev2 ```
    - ```  git reset --hard 6be641e ```
    - ```  git reset --hard HEAD@{0} ```
