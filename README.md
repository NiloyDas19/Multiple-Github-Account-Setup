# **Steps to Clone a Repository from a Specific GitHub Account**

## **Cloning the Repository**

### 1. **Single GitHub Account Setup**

If you have **only one GitHub account** configured on your machine, you can clone the repository directly by running the following command:

```bash
git clone https://github.com/username/gitname.git
```

### 2. **Multiple GitHub Account Setup**

If you have **multiple GitHub accounts** (e.g., a personal account and a work account) configured on your machine, follow these steps to clone repositories from the correct account.

#### **Steps to Setup Multiple GitHub Accounts:**

1. **Generate SSH Keys for Each Account:**

   First, generate a new SSH key for each account. For example, generate a key for your **personal account** and **work account**.

   - For your personal account:
     ```bash
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/id_rsa_personal
     ```

   - For your work account:
     ```bash
     ssh-keygen -t rsa -b 4096 -C "your_email@work.com" -f ~/.ssh/id_rsa_work
     ```

   When prompted, you can leave the passphrase blank or set a passphrase for added security.

2. **Add SSH Keys to the SSH Agent:**

   Next, start the **SSH agent** and add both SSH keys (personal and work):

   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_rsa_personal
   ssh-add ~/.ssh/id_rsa_work
   ```

3. **Configure SSH for Multiple Accounts:**

   To ensure that your machine uses the correct SSH key for each GitHub account, create or edit the `~/.ssh/config` file. Add the following entries:

   ```bash
   # Personal GitHub Account
   Host github_personal
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa_personal

   # Work GitHub Account
   Host github_work
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa_work
   ```

   This configuration tells SSH to use **`id_rsa_personal`** for your **personal account** and **`id_rsa_work`** for your **work account**.

4. **Add SSH Keys to GitHub Accounts:**

   After generating the SSH keys, you need to add the **public keys** to your respective GitHub accounts.

   - For **Personal Account**:
     - Copy the contents of the public key:
       ```bash
       cat ~/.ssh/id_rsa_personal.pub
       ```
     - Go to **GitHub > Settings > SSH and GPG Keys** and add a new key.

   - For **Work Account**:
     - Copy the contents of the public key:
       ```bash
       cat ~/.ssh/id_rsa_work.pub
       ```
     - Go to **GitHub > Settings > SSH and GPG Keys** and add a new key for your work account.

---

#### **Cloning Repositories from Each Account:**

After setting up the SSH keys for both accounts, you can now clone repositories from either account:

1. **Clone from Personal Account** (using `github_personal` alias):

   ```bash
   git clone git@github_personal:username/repository.git
   ```

2. **Clone from Work Account** (using `github_work` alias):

   ```bash
   git clone git@github_work:username/repository.git
   ```

In the commands above:
- Replace `username/repository` with the actual repository and username.
- Use the respective `Host` alias defined in the `~/.ssh/config` file (`github_personal` for your personal account, `github_work` for your work account).

---

## **Post-Cloning Instructions**

Once you have cloned the repository, follow these steps to set up the project:

1. **Navigate into the repository folder**:

   ```bash
   cd client
   ```

2. **Install the project dependencies**:

   ```bash
   npm i --force
   ```

3. **Start the project**:

   ```bash
   npm start
   ```

---

## **Troubleshooting**

1. **SSH Key Issues**:
   - If you encounter issues with SSH authentication, verify that the correct key is being used by running:
     ```bash
     ssh -T git@github.com
     ```
     This should confirm the identity associated with the SSH key.

2. **Switching Between Accounts**:
   - If you need to switch between accounts (e.g., push changes to a repository from your work account after cloning it with your personal account), you can update the remote URL to use the appropriate alias:
     ```bash
     git remote set-url origin git@github_work:username/repository.git
     ```

---

### **Conclusion**

By following the steps above, you can easily manage **multiple GitHub accounts** on your local machine and clone repositories from both accounts. This setup ensures that each account uses its specific SSH key, allowing you to work with both personal and work GitHub accounts seamlessly.
