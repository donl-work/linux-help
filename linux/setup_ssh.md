1. Step 1 — Create the RSA Key Pair

```
ssh-keygen
```

Step 2 — Copy the Public Key to Ubuntu Server

The quickest way to copy your public key to the Ubuntu host is to use a utility called ssh-copy-id

```
ssh-copy-id username@remote_host
```

================================================

# If no ssh-copy-id

Copying Public Key Using SSH
If you do not have ssh-copy-id available, but you have password-based SSH access to an account on your server, you can upload your keys using a conventional SSH method.


```
cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"

```


output in  ssh username@remote_host
```
ssh username@remote_host

username@username-host:~$ ll .ssh/
total 12
drwx------  2 username username 4096 Apr 29 21:51 ./
drwxr-xr-x 31 username username 4096 Apr 29 21:51 ../
-rw-------  1 username username  756 Apr 29 21:51 authorized_keys
````



# Copying Public Key Manually

To display the content of your id_rsa.pub key, type this into your local computer:

```
cat ~/.ssh/id_rsa.pub

```

## Access your remote host using whichever method you have available.

Once you have access to your account on the remote server, you should make sure the ~/.ssh directory exists. This command will create the directory if necessary, or do nothing if it already exists:

```
mkdir -p ~/.ssh
```

Now, you can create or modify the authorized_keys file within this directory. You can add the contents of your id_rsa.pub file to the end of the authorized_keys file, creating it if necessary, using this command:

```
echo public_key_string >> ~/.ssh/authorized_keys
```

In the above command, substitute the public_key_string with the output from the cat ~/.ssh/id_rsa.pub command that you executed on your local system. It should start with ssh-rsa AAAA....

Finally, we’ll ensure that the ~/.ssh directory and authorized_keys file have the appropriate permissions set:

```
chmod -R go= ~/.ssh
```

This recursively removes all “group” and “other” permissions for the ~/.ssh/ directory.

## If you’re using the root account to set up keys for a user account, it’s also important that the ~/.ssh directory belongs to the user and not to root:

```
chown -R sammy:sammy ~/.ssh
```
In this tutorial our user is named sammy but you should substitute the appropriate username into the above command.

We can now attempt passwordless authentication with our Ubuntu server.

# Step 4 — Disable Password Authentication on your Server


`If you were able to log into your account using SSH without a password, you have successfully configured SSH-key-based authentication to your account`. However, your password-based authentication mechanism is still active, meaning that your server is still exposed to brute-force attacks.


```
sudo nano /etc/ssh/sshd_config
```


Inside the file, search for a directive called `PasswordAuthentication`. This may be commented out. Uncomment the line and set the value to `no`. This will disable your ability to log in via SSH using account passwords:

```
PasswordAuthentication no
```

Save and close the file ` CTRL + X, then Y to confirm saving the file, and finally ENTER to exit nano`


`Restart the sshd service:`

```
sudo systemctl restart ssh
```

