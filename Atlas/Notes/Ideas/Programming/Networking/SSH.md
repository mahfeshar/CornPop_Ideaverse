---
up:
  - "[[Networking Fundamentals]]"
related: 
created: 2024-07-23
Link: https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys
---

- SSH(Secure Shell) is a secure protocol used as the primary means of connecting to **Linux [[Server|servers]] remotely**.
- It provides a safe and secure way of **executing commands**, **making changes**, and **configuring services** remotely
## How SSH Works
- أول ما تعمل Connect أي أمر هتكتبه هيتنفذ على الـ Remote server
- The SSH connection is implemented using a [[Client-Server Architecture|Client-server model]].
	- To establish an SSH connection, the remote machine requires an SSH daemon software. This daemon listens on a designated network port, handles incoming connection requests, verifies user credentials, and initiates the requested session environment upon successful authentication.
	- The user’s computer must have an SSH client. This is a piece of software that knows how to communicate using the SSH protocol and can be given information about the remote host to connect to, the username to use, and the credentials that should be passed to authenticate.

## How SSH Authenticates Users
في الـ SSH، لما تحاول توصل لجهاز بعيد، لازم يكون الجهاز ده عامل حاجة اسمها "SSH daemon". ده برنامج بيستنى اتصالات على رقم معين على الشبكة. البرنامج ده بيتأكد إنك ممكن تتصل بيه بطريقة صحيحة، بيتأكد من كلمة السر اللي بتدخلها أو من مفاتيح SSH.

الكلمات السرية سهلة وبسيطة لكنها مش آمنة كفاية. برامج الهاكرز والبرمجيات الضارة بتحاول بشكل متكرر تخمين الكلمات السرية، اللي ممكن يؤدي لتعرض الأمان. عشان كده، من الأفضل استخدام مفاتيح SSH لأمان أكبر.

---
- مفاتيح SSH عبارة عن زوج من الرموز السرية. 
	- الرمز العام (public) ممكن تشاركه بحرية. 
	- بينما الرمز الخاص (private) لازم يتم حفظه وحمايته بعناية. 
	- عشان تستخدم مفاتيح SSH، لازم تكون عندك الاثنين على جهازك. 

- On the remote server, the public key must be copied to a file within the user’s home directory at `~/.ssh/authorized_keys`. 
- This file contains a list of public keys, one-per-line, that are authorized to log into this account.

- لما تحاول تتصل باستخدام مفاتيح SSH، 
	- جهازك بيقول للسيرفر إنه هيستخدم مفتاح معين public (بيحدد أي واحد منهم بالظبط). 
	- السيرفر بيتأكد إن ده المفتاح الصح في ملف `authorized_keys` بتاعه. 
	- بعدين، السيرفر بيبعت رسالة سرية لجهازك، بيشفرها بالمفتاح العام بتاعك.
	- جهازك بيفك تشفير الرسالة السرية دي باستخدام **Private key**. 
	- بعدين، بيجمعها مع رقم جلسة وبيرجعها للسيرفر. 
	- السيرفر بيتأكد إن الرسالة اللي بعتها تطابق اللي بعتها قبل كده. 
	- لو كله تمام، يعني إنك عندك المفتاح الخاص الصحيح.

ده هو اللي بيحافظ على أمان اتصالاتك بدون ما تحتاج تكتب كلمة سر كل مرة.

## Working with SSH Keys
### Generating an SSH Key Pair
- A number of cryptographic algorithms can be used to generate SSH keys, including RSA, DSA, and ECDSA. RSA keys are generally preferred and are the default key type.

To Generate an RSA key:
```sh
ssh-keygen
ssh-keygen -t rsa


Generating public/private rsa key pair.
Enter file in which to save the key (/home/demo/.ssh/id_rsa):
# choose the location to store your RSA private key.

#Press `ENTER` to leave this as the default, which will store them in the `.ssh` hidden directory in your user’s home directory.

Enter passphrase (empty for no passphrase):
Enter same passphrase again:
# you will have to enter any passphrase you set here every time you use the private key
```

This procedure has generated an RSA SSH key pair located in the `.ssh` hidden directory within your user’s home directory. These files are:

- `~/.ssh/id_rsa`: The private key. DO NOT SHARE THIS FILE!
- `~/.ssh/id_rsa.pub`: The associated public key. This can be shared freely without consequence.

---
```sh
ssh-keygen -b 4096 # change bits number (Larger)

-f school # Name of the created private key
-N betty # The created key must be protected by the passphrase `betty`
```

### Removing or Changing the Passphrase on a Private Key
```sh
ssh-keygen -p

Enter file in which the key is (/root/.ssh/id_rsa):

Enter old passphrase:

Enter new passphrase (empty for no passphrase):
Enter same passphrase again:
```

### Copying your Public SSH Key to a server
#### With `ssh-copy-id`
```sh
ssh-copy-id username@remote_host
```

After typing in the password, the contents of your `~/.ssh/id_rsa.pub` key will be appended to the end of the user account’s `~/.ssh/authorized_keys` file:

```sh
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'demo@111.111.11.111'"
and check to make sure that only the key(s) you wanted were added.
```

You can now log in to that account without a password:
```sh
ssh username@remote_host
```
#### Manually
```sh
cat ~/.ssh/id_rsa.pub
ssh-rsa *******
```

You can copy this value, and manually paste it into the appropriate location on the remote server.
You will have to log in to the remote server through other means

**On the remote server**, create the `~/.ssh` directory if it does not already exist:
```sh
mkdir -p ~/.ssh
echo public_key_string >> ~/.ssh/authorized_keys
```


Summary:
```sh
# In server
ssh ubuntu@your_server_ip
mkdir -p ~/.ssh
chmod 700 ~/.ssh
echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAvf... user@example.com" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
cat ~/.ssh/authorized_keys

```
## Configuration File
Watch this : [SSH Crash Course | With Some DevOps - YouTube](https://www.youtube.com/watch?v=hQWRp-FdTpc)

A configuration file for SSH (Secure Shell) is used to **define settings and preferences** for SSH client connections. 
There are typically two types of configuration files: the global configuration file and the user-specific configuration file.
Here’s a comprehensive overview of what you need to know:

### 1. Global Configuration File
- **Location:** `/etc/ssh/ssh_config`
- **Purpose:** This file sets the default configuration for all users on the system.
- **Permissions:** Typically requires root privileges to edit.

### 2. User-Specific Configuration File
- **Location:** `~/.ssh/config`
- **Purpose:** This file sets configuration options specific to an individual user.
- **Permissions:** Should be owned by the user and not writable by others.

### Key Directives and Options

Here are some commonly used directives and options you might configure in an SSH configuration file:

1. **Host**
   - **Purpose:** Specifies which hosts the configuration section applies to.
   - **Example:**
     ```sh
     Host github.com
     ```

2. **HostName**
   - **Purpose:** Specifies the real host name to log into.
   - **Example:**
     ```sh
     HostName github.com
     ```

3. **User**
   - **Purpose:** Specifies the user to log in as.
   - **Example:**
     ```sh
     User git
     ```

4. **Port**
   - **Purpose:** Specifies the port number to connect to on the remote host.
   - **Example:**
     ```sh
     Port 22
     ```

5. **IdentityFile**
   - **Purpose:** Specifies a file from which the user’s identity (private key) is read.
   - **Example:**
     ```sh
     IdentityFile ~/.ssh/id_rsa
     ```

6. **ProxyCommand**
   - **Purpose:** Specifies the command to use to connect to the server.
   - **Example:**
     ```sh
     ProxyCommand ssh -W %h:%p gateway.example.com
     ```

7. **ServerAliveInterval**
   - **Purpose:** Specifies the interval (in seconds) to send a message to the server to keep the connection alive.
   - **Example:**
     ```sh
     ServerAliveInterval 60
     ```

8. **ServerAliveCountMax**
   - **Purpose:** Specifies the number of server alive messages (see above) which may be sent without receiving any messages back from the server.
   - **Example:**
     ```sh
     ServerAliveCountMax 3
     ```
 9. **PasswordAuthentication**
   - **Purpose:**  refuse to authenticate using a password
   - **Example:
     ```sh
    PasswordAuthentication no
     ```
### Example Configuration File

Here's an example of what a user-specific configuration file might look like:

```sh
# Default for all hosts
Host *
    ForwardAgent yes
    ForwardX11 yes
    ServerAliveInterval 60
    ServerAliveCountMax 3

# GitHub configuration
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_github

# Internal server
Host internal-server
    HostName 192.168.1.100
    User admin
    Port 2222
    IdentityFile ~/.ssh/id_rsa_internal
    ProxyCommand ssh -W %h:%p gateway.example.com
```

### Tips for Using SSH Configuration Files

1. **Security:** Ensure that your SSH private key files (e.g., `~/.ssh/id_rsa`) have the correct permissions. They should be readable only by the owner (`chmod 600 ~/.ssh/id_rsa`).

2. **Multiple Keys:** If you use multiple SSH keys, you can specify different keys for different hosts using the `IdentityFile` directive.

3. **Aliases:** Use the `Host` directive to create easy-to-remember aliases for your frequently accessed servers.

4. **Testing Configuration:** You can test your SSH configuration with the command:
   ```sh
   ssh -G <hostname>
   ```
   This will print the configuration that SSH would use for that host, allowing you to verify your settings.

By configuring your SSH client with these options, you can streamline your connection process and enhance security.