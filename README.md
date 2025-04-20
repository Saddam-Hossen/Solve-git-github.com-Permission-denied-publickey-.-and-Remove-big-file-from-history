# Solve-git-github.com-Permission-denied-publickey-.-and-Remove-big-file-from-history

Sure! Here's a clean overview of both parts you're asking for:

---

## ✅ **Overview of Solving `git@github.com: Permission denied (publickey)`**  
**(Solution by Abdul, simplified)**

This error usually happens when GitHub can't verify your SSH key. Here's how Abdul solved it:

### 🔧 **Steps:**

1. **Start the SSH Agent**
   ```bash
   eval $(ssh-agent -s)
   ```
   ➤ This starts the background service that handles your SSH keys.

2. **Add your SSH private key**
   ```bash
   ssh-add ~/.ssh/saddamnvn
   ```
   ➤ This adds your custom SSH key (`saddamnvn`) to the agent so GitHub can use it.

3. **Test GitHub SSH connection**
   ```bash
   ssh -T git@github.com
   ```
   ➤ You should see:
   > *Hi Saddam-Hossen! You've successfully authenticated, but GitHub does not provide shell access.*

---

### ✅ Then continue with Git commands:

4. **Pull latest changes**
   ```bash
   git pull origin main
   ```

5. **Stage all changes**
   ```bash
   git add .
   ```

6. **Commit your changes**
   ```bash
   git commit -m "your comment"
   ```

7. **Push your code**
   ```bash
   git push origin main
   ```

---

## 🧹 **Overview of Removing a Large File from Git History (`attendance.tar`)**

GitHub blocks files over **100 MB**, and your `attendance.tar` is ~475 MB. Even if removed from the folder, **it still exists in history** — so you must clean it.

### 🔥 Step-by-step Fix:

1. **Untrack the large file**
   ```bash
   git rm --cached attendance.tar
   ```

2. **Ignore it forever**
   ```bash
   echo "attendance.tar" >> .gitignore
   git add .gitignore
   git commit -m "Remove attendance.tar and added to .gitignore"
   ```

3. **Delete it from all previous commits**
   ```bash
   git filter-branch --force --index-filter \
   "git rm --cached --ignore-unmatch attendance.tar" \
   --prune-empty --tag-name-filter cat -- --all
   ```

4. **Force push cleaned repo**
   ```bash
   git push origin --force
   ```

---

### 🎯 Summary:

| Problem                            | Fix                                                                 |
|-----------------------------------|----------------------------------------------------------------------|
| Permission denied (publickey)     | Start SSH agent → Add key → Test with `ssh -T git@github.com`       |
| Large file (>100MB) blocks push   | Remove file from history using `filter-branch`, then force push     |

