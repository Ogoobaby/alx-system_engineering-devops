0x06. SSH
0. Use a private key mandatory

Write a Bash script that uses ssh to connect to your server using the private key ~/.ssh/holberton with the user ubuntu.

Requirements:

    Only use ssh single-character flags
    You cannot use -l
    Do not need to handle the case of a private key protected by a passphrase

1. Create a SSH key pair mandatory

Write a Bash script that creates a RSA key pair.

Requirements:

    Name of the created private key must be holberton
    Number of bits in the created key to be created 4096
    The created key must be protected by a passphrase

Example:
2. Client configuration file mandatory

Your Ubuntu Vagrant machine has an SSH configuration file for the local SSH client, let’s configure it to our needs so that you can connect to a server without typing a password. Share your SSH client configuration in your answer file.

Requirements:

    Your SSH client configuration must be configured to use the private key ~/.ssh/holberton
    Your SSH client configuration must be configured to refuse to authenticate using a password

Example:
3. Let me in! mandatory

Now that you successfully connect to your server, we would also like to join the party.

Add the SSH public key bellow to your server so that we can connect using the ubuntu user.
