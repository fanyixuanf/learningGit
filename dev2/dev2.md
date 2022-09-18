## dev2
- ``` git checkout -b dev2 origin/main ```
- ``` git pull origin dev ``` 回滚方案
  - ``` git reflog ```
    - ``` 6be641e (HEAD -> dev2, origin/dev2) HEAD@{0}: checkout: moving from dev to dev2 ```
  - ```  git reset --hard 6be641e ```
  - ```  git reset --hard HEAD@{0} ```
