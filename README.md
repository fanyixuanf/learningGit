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
    - ``` git commit --amend --only ```
    - ``` git push origin dev --force ```
    
### 单次提交里的用户名和邮箱不对
- ``` git commit --amend --author "schadenfreude <schadenfreudef@gmail.com>" ```

### 从一个提交里移除一个文件
- ``` 
  git checkout HEAD^ dev2/dev2.md
  git add -A
  git commit -m ""
  git push origin dev
  ```
- ``` 
  git checkout HEAD^ dev2/dev2.md
  git add -A
  git commit --amend 
  git push origin dev
  ```

### 删除最后一次提交
- 已push
  - 不到万不得已的时候不要这么做
  ```
     git reset HEAD^ --hard 
     git push -f
  ```
  - 推荐
  ``` 
  git revert SHA of commitid
  ```
- 未push
  - ```
    git reset --soft HEAD@{1} 
    ```
### 删除任意提交
- 不到万不得已的时候不要这么做
  - ``` 
    git rebase --onto SHA_OF_BAD_COMMIT^ SHA_OF_BAD_COMMIT  
    git push -f   
    ```
- 推荐
  - ``` git revert SHA of commitid ```

### 尝试push一个修正后的提交(amended commit)到远程，但是报错：
- *要避免强推*
- ``` 
  To github.com:fanyixuanf/learningGit.git
  ! [rejected]        dev -> dev (non-fast-forward)
  error: failed to push some refs to 'github.com:fanyixuanf/learningGit.git'
  hint: Updates were rejected because the tip of your current branch is behind
  hint: its remote counterpart. Integrate the remote changes (e.g.
  hint: 'git pull ...') before pushing again.
  hint: See the 'Note about fast-forwards' in 'git push --help' for details.
  ```
  - ``` git push origin dev -f ``` or ``` git push origin mybranch --force  ```

### 做了一次hard reset后，想找回这次提交
- ``` 
  git reflog
  git reset --hard SHA1234
  ```

### 提交文件的一部分，而不是这个文件的全部
- ```  git add --patch filename.x  ``` or ``` git add -p filename.x ```
- ``` git add -N filename.x ```
- ``` git add -p ```

### 把暂存的内容变成未暂存，把未暂存的内容暂存起来
- ``` 
   git commit -m "WIP"  
   git add .  
   git stash  
   git reset HEAD^  
   git stash pop --index 0
  ```

### 把未暂存的内容移动到一个新分支
- ``` git checkout -b dev1 ```

### 把未暂存的内容移动到另一个已存在的分支
- ```
   git stash  
   git checkout dev
   git stash pop
  ```
  
### 丢弃本地未提交的变化
- ```
  # one commit  
  git reset --hard HEAD^
  # two commits
  git reset --hard HEAD^^
  # four commits
  git reset --hard HEAD~4
  # or
  git checkout -f
  ```

### 丢弃某些未暂存的内容
- ``` git checkout -p
  git checkout -p
  # or
  git stash -p
  git reset --hard
  git stash pop
  # or
  git stash -p
  git stash drop
  ```