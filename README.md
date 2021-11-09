# SSH Group Tutorial

In this quick little tutorial, you will:
- SSH into a friend's virtual machine
- Leave a nice message on their file system for them to read

## Create an SSH key pair

The first thing each of you will need to do is generate a fresh SSH key pair.

You will use this key pair to authenticate yourselves to access your friend's virtual machine.

To generate a key pair, run:

```bash
cd
ssh-keygen
```

You will be prompted with the following message:

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/<your_user_here>/.ssh/id_rsa): 
```

Enter the following path:

```
.ssh/my-new-key
```

When it prompts you for a passphrase, leave the text entry blank and just hit return until you see the following:

```text
Your identification has been saved in .ssh/my-new-key
Your public key has been saved in .ssh/my-new-key.pub
The key fingerprint is:
SHA256:foJa0TBY57owdmSV3SoCt6pVAZByxnLMtMgU2WxYpL4 <your-user>@<your-server>
The key's randomart image is:
+---[RSA 3072]----+
| B@=... oo .     |
|=+X=.oo+. . .    |
|.Oo .o=o.  .     |
|.    o+=. .      |
| .  +o+.S.       |
|  ..o+ =         |
| E o  + o .      |
|  .  o   o       |
|    .            |
+----[SHA256]-----+
```

Check that your key pair had been created by running:

```bash
ls -la ~/.ssh
```

You should see two files called `my-new-key` (the private key) and `my-new-key.pub` (the public key).

We will need the contents of `my-new-key.pub` for later, so print the contents out using:

```bash
cat ~/.ssh/my-new-key.pub
```

Copy and paste this to a notepad for later.

## Create a user on your VM

Next, we want to create a user on your VM for your friend to connect as via SSH.

Run this command to create the user, replacing `<username>` with your friend's name:

```bash
sudo useradd -m -s /bin/bash <username>
```

Now, log in as this user:

```bash
sudo su - <username>
```

To allow your friend to log in as this user on your machine, you need to paste the contents of *their* `my-new-key.pub` (their public key) file.

Ask them to send their public key to you. Then, open the file `~/.ssh/authorized_keys` in a text editor of your choice and paste their public key in that file.

## SSH into your friend's VM

Finally, let's SSH into your friend's VM.

Run the following command to SSH from your VM into your friend's VM:

```bash
ssh -i ~/.ssh/my-new-key <username>@<your_friend's_vm's_public_ip>
```

> Remember: `<username` in this case is the user that your friend made for you on their VM!

If your connection was successful, you should see the command prompt change to say `<username>@<your_friend's_vm_name`.

Finally, leave a lovely compliment in a text file on their file system!

```bash
echo "Your hair looks lovely today!" > nice-message.txt
```

When you're done, log out of their machine by entering:

```bash
exit
```

Now, go see the message your friend has left for you! Remember that the message will be create under the user you made for your friend, so you may have to switch back to that user to see it.
