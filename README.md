# Client Repository Setup Guide

## Cloning the Repository

### 1. **Single GitHub Account Setup**

If you have **only one GitHub account** configured on your machine, you can clone the repository directly by running the following command:

```bash
git clone https://github.com/dojoit/client.git
```

### 2. **Multiple GitHub Account Setup**

If you have already logged in with your personal GitHub account on your machine, follow these steps to configure multiple GitHub accounts:

#### Steps to Setup Multiple GitHub Accounts:

1. **Generate SSH Keys for Each Account:**
   Generate a new SSH key for your second (work) account:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@work.com" -f ~/.ssh/id_rsa_work
   ```

2. **Add SSH Keys to the SSH Agent: Start the SSH agent and add both keys:**

   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_rsa_personal
   ssh-add ~/.ssh/id_rsa_work
   ```

3. **Configure SSH for Multiple Accounts: Open or create the SSH config file `(~/.ssh/config)` and add these entries:**

   ```bash
   Host github_personal
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa_personal

   Host github_work
       HostName github.com
       User git
       IdentityFile ~/.ssh/id_rsa_work
   ```

#### After setup multiple GitHub account, you can clone the repository using following command:

```bash
git clone git@github_work:username/repo.git
```

## Post-Cloning Instructions

Once you have cloned the repository, follow these steps to install the necessary dependencies and run the project:

1. Navigate into the repository folder:

   ```bash
   cd client
   ```

2. Install the project dependencies:

   ```bash
   npm i --force
   ```

3. Start the project:
   ```bash
   npm start
   ```
