# web-dev

## SSH Basics

My personal website is hosted on _GoDaddy.com_. I wanted a way to connect to it from my own machine. There were a few steps before I could SSH in.

GoDaddy uses cPanel, a web-based, point-and-click dashboard that's bundled with their hosting plans. Before I could connect to my site, I had to enable SSH in the cPanel's main dashboard. Here's more info on what can be managed within cPanel.

| Area                  | Typical tools you’ll see                                                           |
| --------------------- | ---------------------------------------------------------------------------------- |
| **Files & access**    | File Manager, FTP Accounts, SSH Access (where you enabled shell and uploaded keys) |
| **Domains & DNS**     | Add-on Domains, Subdomains, Zone Editor                                            |
| **Email**             | Create mailboxes, spam filters, autoresponders                                     |
| **Databases**         | MySQL/PostgreSQL, phpMyAdmin                                                       |
| **Security**          | SSL/TLS, IP Blocker, Two-Factor Auth                                               |
| **Software & apps**   | Softaculous 1-click installers for WordPress, etc.                                 |
| **Metrics & backups** | Bandwidth stats, raw logs, site and database backups                               |

Once I enabled access, I then went into the SSH Access settings and created a new key. The cPanel settings page has this helpful description:

> The public and private key are similar to a puzzle. They are created together to use during the login/authentication process. The public key resides on the server (the remote location). The private key resides locally on your computer/server. When you attempt to login to a server, the public and private key are compared. If they match, then you will be allowed to login to the server location.

I downloaded the private key to my local machine and chmod 600'd it using this command:

```chmod 600 ~/.ssh/private_key```

chmod stands for "Change Mode", the Unix command for setting file permissions. ```chmod 600``` makes the file readable and writable only by you; everyone else gets nothing. OpenSSH refuses to use a private key if it can be viewed or modified by other users. Otherwise anyone with local access could copy the key and log in as you.

I then connected to the server from my Mac Terminal using ```ssh -i ~/.ssh/private_key yourUser@yourWebsite```. The -i in the command tells SSH which private-key file to use.

I'm then prompted to enter my password (which I also set up in cPanel), and I was in!
