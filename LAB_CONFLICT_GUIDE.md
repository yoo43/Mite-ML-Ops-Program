# 🤝 Git Collaboration & Pull Request Conflict Demo

This guide is specifically tailored for **Yogesh (PC 1)** and **Friend (PC 2)** collaborating on:  
`https://github.com/yoo43/Mite-ML-Ops-Program`

---

## 📌 Phase 1: Push the Demo Branch (Yogesh - PC 1)

In your terminal on PC 1 inside this directory:
```bash
git push -u origin collab-conflict-demo
```
*(If prompted, sign in via browser or Personal Access Token to authenticate with your GitHub account).*

---

## 📌 Phase 2: Friend Pulls/Clones on PC 2

On your friend's PC (PC 2):
```bash
# 1. Clone the repository
git clone https://github.com/yoo43/Mite-ML-Ops-Program.git
cd Mite-ML-Ops-Program

# 2. Switch to the demo branch
git checkout collab-conflict-demo
```

---

## 📌 Phase 3: Creating the Conflict Scenario

Both of you will now edit **Line 2 of `hello.py`** differently!

### 🧑‍💻 1. Yogesh (PC 1) makes changes & pushes:
Open `hello.py`:
```python
def greet():
    message = "Hello from Yogesh (PC 1)!"
    print(message)

if __name__ == "__main__":
    greet()
```
Run:
```bash
git add hello.py
git commit -m "Update greeting message by Yogesh"
git push origin collab-conflict-demo
```
✅ *Yogesh's changes are now live on GitHub.*

---

### 🧑‍💻 2. Friend (PC 2) makes changes to the SAME line (Without Pulling!):
On PC 2, open `hello.py` and modify line 2:
```python
def greet():
    message = "Hello from Friend (PC 2)!"
    print(message)

if __name__ == "__main__":
    greet()
```
Friend commits locally:
```bash
git add hello.py
git commit -m "Update greeting message by Friend"
```

Friend attempts to push:
```bash
git push origin collab-conflict-demo
```
❌ **Rejected!** Git will reject the push:
```text
! [rejected]        collab-conflict-demo -> collab-conflict-demo (fetch first)
error: failed to push some refs
```

---

## 📌 Phase 4: Friend Pulls to Trigger the Conflict

Since Git rejected the push, Friend must pull from GitHub:
```bash
git pull origin collab-conflict-demo
```

💥 **Merge Conflict Output:**
```text
Auto-merging hello.py
CONFLICT (content): Merge conflict in hello.py
Automatic merge failed; fix conflicts and then commit the result.
```

---

## 📌 Phase 5: Inspect & Resolve the Conflict (Friend - PC 2)

Open `hello.py`. Git marks both conflicting edits:
```python
def greet():
<<<<<<< HEAD
    message = "Hello from Friend (PC 2)!"
=======
    message = "Hello from Yogesh (PC 1)!"
>>>>>>> commit_hash
    print(message)

if __name__ == "__main__":
    greet()
```

### To Resolve:
1. Delete `<<<<<<< HEAD`, `=======`, and `>>>>>>>`.
2. Decide on the combined greeting:
   ```python
   def greet():
       message = "Hello from Yogesh and Friend!"
       print(message)

   if __name__ == "__main__":
       greet()
   ```
3. Mark as resolved, commit, and push:
   ```bash
   git add hello.py
   git commit -m "Resolve merge conflict between Yogesh and Friend"
   git push origin collab-conflict-demo
   ```

---

## 📌 Phase 6: Creating the Pull Request (PR) on GitHub

Now that the branch is updated, create a Pull Request on GitHub:
1. Open [https://github.com/yoo43/Mite-ML-Ops-Program](https://github.com/yoo43/Mite-ML-Ops-Program).
2. You will see a banner: **"collab-conflict-demo had recent pushes"** with a green button: **Compare & pull request**.
3. Click **Compare & pull request**.
4. Set:
   - **Base:** `main`
   - **Compare:** `collab-conflict-demo`
5. Title: `Add hello.py with resolved collaboration greeting`
6. Click **Create pull request**.
7. In the lab, show your instructor that:
   - The Pull Request is clean with no conflicts (`Able to merge`).
   - The commit history shows both contributions and the merge conflict resolution commit!
8. Click **Merge pull request** -> **Confirm merge**.

---

## 📌 Phase 7: Sync PC 1 (Yogesh)
Back on PC 1, pull the final code:
```bash
git pull origin collab-conflict-demo
```
Both PCs and GitHub are now completely in sync! 🎉
