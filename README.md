# learningGit

### 创建branch
- ```git checkout -b dev origin/main```
- ``` git checkout -b dev2 origin/main ```

### 删除远程branch
- ``` git push --delete origin dev2 ```

### 删除本地branch
-  ```  git branch -D dev2  ```

### 我从错误的分支拉取了内容，或把内容拉取到了错误的分支
- ``` On branch dev2 ```
- ``` git pull origin dev ``` 拉取错误的分支
    - ``` git reflog ```
        - ``` 6be641e (HEAD -> dev2, origin/dev2) HEAD@{0}: checkout: moving from dev to dev2 ```
    - ```  git reset --hard 6be641e ```
    - ```  git reset --hard HEAD@{0} ```

### 显示当前 ```HEAD```上的最近一次的提交(commit)
- ``` git show ```
- ``` git log -n1 -p  ```

### 修改提交信息commit message
- 未push
  - ``` git commit --amend --only ```
- 已push
  - 修改commit message后 ```force push```

