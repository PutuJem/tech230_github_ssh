# Connecting to GitHub with SSH (Secure SHell)

### **Generating a new SSH key**

1. Open a Git Bash terminal and navigate to the `.ssh` folder; if not present, create an `.ssh` folder with `mkdir`. Following this, generate an SSH key with the following command:

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
>Note: rsa is a widely used public-key algorithm for SSH key and 4096 is a typical bit size for a key.

2. The user is then prompted to enter a file name to store the key in.

```
> Enter a file in which to save the key (/c/Users/YOU/.ssh/id_ALGORITHM):<file_name>
```

3. A passphrase may also be used for security, this example does not utilise a passphrase.

```
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

>An example of the terminal output after the SSH key is generated.
```
Your identification has been saved in <file_name>
Your public key has been saved in <file_name>.pub
The key fingerprint is:
SHA_no:key <email_address>
The key's randomart image is:
+---[RSA_No]----+
| .*oo   o+...+*= |
|.*o= o o .=.+=o E|
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
|                 |
+----[SHA_No]-----+
```

### **Authenticating the key on GitHub**

4. Navigate to the GitHub webpage and login.

5. Navigate to `settings` then the `SSH and GPG key` tab.

6. Create a new SSH key by clicking `New SSH key`.

7. Within your bash terminal, display the public key and copy it with:

```bash
cat <ssh_file_name>.pub
```

8. Name the key in the `Title` entry and paste the key into the `key` entry, keep the key type as `Authentication Key`.

>Note: Becareful when copying the key to ensure no white spaces are present.

9. Finally, click `Add SSH key`.

### **Run the SSH agent and add the key**

10. Within the bash terminal, configure the environment and instruct the shell to the `ssh-agent` with command:

```bash
$ eval "$(ssh-agent -s)"
```
>The following is an example output.

![agent](agentpip.PNG)

11. Add the SSH key to the `ssh-agent` with the following:

```bash
$ ssh-add ~/.ssh/<ssh_file_name>
```

12. Check the SSH connection and key authentication with:

```bash
$ ssh -T git@github.com
```

>The following message should be displayed in the terminal.

```
Hi <user_name>! You've successfully authenticated, but GitHub does not provide shell access.
```

13. You should now be able to clone the repository or connect an existing repository through SSH with the following commands:

>Clone the GitHub repository:

```bash
$ git clone git@github.com:<user_name>/<ssh_file_name>.git
```

>Add an existing repository:

```bash
$ git remote add origin git@github.com:<user_name>/<github_repository>.git
```