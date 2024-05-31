# Phishing for dummies

-----

The author of this document is <strong>miblak</strong>.


## What is Phishing?
Phishing is a fraud method that involves impersonating a trusted institution or person (e.g. a bank, courier company or public figure) in order to persuade the victim to perform an action for the benefit of the attacker, e.g. providing login details or downloading a malicious file. Most phishing attacks use social engineering. Through it, the attacker tries to make us fear (e.g. information about legal problems in the event of non-payment of an invoice), embarrassment (e.g. news that someone has gained access to our private information) or euphoria (e.g. a message informing us about big win).

<br>

## Types of Phishing

- **Phishing** - a basic attack involving impersonation of a trusted institution or person. This attack is often directed at a certain group of people.
  
- **Spear Phishing** - Spear phishing attacks target a single user. The attacker puts much more effort into learning about the victim, including details of his job, people he regularly contacts, and activities he does in his free time. This allows an attacker to send a highly personalized email that is much harder to detect.

- **Whaling** - this is a phishing scam targeting high-level employees. During whaling attempts, attackers use spear phishing techniques to attack management staff and extort, for example, large-dollar transfers.
  
- **Pharming** - is a type of phishing in which people who want to visit a real website are redirected to a fake website. This attack occurs when DNS server security is breached or DNS addresses are replaced with the criminal's addresses.
  
- **Smishing** - phishing via SMS. When smishing, the attacker applies the same principles as with regular phishing.
  
- **Vishing** - voice phishing. An attack in which criminals call the victim (often spoof the bank's telephone number) in order to extort data.

<br>

## Cybercriminals tricks

- **Browser in the Browser (BiTB)** - This technique involves displaying a seemingly new window as part of the visited site, which contains a fake login panel. In fact, the displayed window is part of the page, thanks to which the visible address of the new window is actually a regular text controlled 100% by the attacker. Thanks to this, the user may be convinced that he logs on the real page, especially since nowadays logging in using third pages, e.g. Facebook, Twitter, Github is not new (in the case of such login we can observe a "pop -up" new window in which we have to log in). PoC: [https://github.com/mrd0x/BITB](https://github.com/mrd0x/BITB)
  
- **Intelligent links shorteners** - The link shorteners we know work in a fairly simple and well-known way, but it is worth knowing that there are much more sophisticated shorteners than the ones we know. There are shorteners that can deceive websites that "expand" links, thanks to which such websites can inform us that a given shortened link actually leads to, for example, a banking website. In addition, such shorteners can redirect users to different pages depending on the device on which the link is opened, making the attack more targeted and harder to detect.
  
- **Using trusted pages to embed malware / phishing pages** - Attackers are increasingly using popular, and therefore trusted, websites to carry out, among others, phishing attacks. By using such websites, criminals effectively reduce our vigilance. As part of this technique, they embed malicious files in known websites or create fake login pages. A full list of such sites can be found at: [https://lots-project.com/](https://lots-project.com/).


Regardless of the technique used, it is important that our phishing domain is as similar to the real one as possible. The best solution would be if the difference was only in the TLD (e.g. the real website is example.com and we are buying the example.net domain). However, if purchasing such a domain is not possible or the TLD looks suspicious (e.g. .website etc.), it is worth trying to buy a domain that differs by e.g. one letter (e.g. haveibeenpwned.com vs haveibeenpwnd.com). **If your only experience with phishing so far has been using ready-made templates and the link to the website resembled a clumsy cluster of numbers and letters, forget about it! It's time to prepare a real phishing attack!**

Additionally, to ensure that our phishing messages do not fall into spam and that all filters do not block them, we must ensure a number of security measures for our messages and the environment. Because each message sent is checked for correct HTML, SPF, DKIM, DMARC, rDNS or even a header indicating the possibility of unsubscribing from the "newsletter" (each of these and other security measures / settings are scored appropriately). Of course, we will not allow anyone to actually unsubscribe from our e-mail list, but these seemingly trivial settings will allow us to create phishing messages that will always go straight to the main folder, which will only help us in extorting data. 

<br>

Enough theory! Let's start preparing the best phishing environment you've ever seen! On the following pages, I will guide you through the entire process of creating a phishing. We will start with purchasing a domain, VPS, and finish with sending the first campaign! It is important that you know at least the basics of Linux.

<br>

## Step by Step part
### 1. Domain purchase

At the very beginning, we must consider what we want to achieve with phishing. What site do we want to impersonate? Do we want to extort data? Maybe we want to convince our victim to download a malicious attachment that will infect the device? Regardless of your intentions, we need a domain from the very beginning! It will be used to create an e-mail address from which we will send the message, and it will also be the address to which your victim will go. Think carefully about your choice, think about which domain will most convince someone to visit a given address.

<br>

In the example below, I will prepare a scenario in which the victim will receive a message informing about his data being leaked. Using the link provided, she will allegedly be able to check what data was leaked and from where. In this scenario, I will impersonate the domain haveibeenpwned.com and use the domain haveibeenpwnd.pl that I purchased earlier. To buy/register your own domain, you can use many websites, e.g. home.pl, sldc.eu or ovhcloud.com (there are many more similar websites). Depending on your choice, the process of purchasing/configuring DNS etc. may vary slightly. After purchasing the domain and registering your account, you will have access to DNS in which we will be able to indicate where the victim should be directed after entering the name of our website in the browser.

<br>

### 2. VPS Purchase

VPS, or Virtual Private Server, is the place where we will soon configure our phishing infrastructure. Thanks to the VPS, we will obtain a public IP, which will allow our domain to direct victims to a specific address. However, first we need to buy a VPS. So type VPS into Google and browse the offers. I used SDC-KVM-100G from sldc.eu (**It is important that you choose Debian 10 as your OS - I will be working on this system**)

If in both cases you used the sldc.eu website, you will receive an e-mail with your first password to the panel to the e-mail address you provided during registration. After logging in, go to **Virtual Servers -> press "Manage" next to your domain -> Root/Admin Password -> change** which will allow you to create a new SSH password (note: in the next steps I do not focus on the security of the VPS itself' a. Therefore, it is worth prohibiting logging in directly to the root account, and forcing logging in only using keys).

<br>

### 3. First DNS configuration

Go to the VPS panel, then go to **DNS -> press "Manage" next to your domain**. At this point we need to add 4 records to our DNS. The first two records are responsible for indicating the Name Servers (the names of these NSs should be received when purchasing the domain) used by our domain (NS record), the next two indicate the IP address (A record) to which someone is to connect after entering the address of our domain ( here we indicate the IP address of our VPS). If you want to know other records, you can read about them at the following link: [https://www.cloudflare.com/learning/dns/dns-records/](https://www.cloudflare.com/learning/dns/dns-records/)

<br>

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/dns.png">
</p>


<br>

After setting the records, go to **Virtual Servers -> press "Manage" next to your domain -> Network** and set the rDNS to point to your domain name. A word of explanation: DNS translates the domain into an IP address (you can check this by entering `host domain.pl` in the terminal, where instead of domain.pl, enter your domain). rDNS is the opposite of the earlier example. The rDNS setting is therefore responsible for indicating the domain address after querying the IP address. So it's time to log in to our VPS!

<br>

### 4. Login in to the VPS

To log in to our VPS, go to the terminal and enter:
<br>
```
ssh root@<ip> -p <port>
```
<br>

Of course, instead of **&lt;ip&gt;** enter the IP address of your VPS, and instead of **&lt;port&gt;** port number on which SSH runs. If SSH works on the default port 22, you can use the command `ssh root@<ip>`. After pressing enter, we will be asked to enter the password (input will not be shown, so we may have the impression that nothing is being entered). If you did everything right, you will be connected to SSH. The first time you connect, it is worth updating our system. So let's type:
<br>

```
apt-get update -y && apt-get dist-upgrade -y
```
<br>

### 5. Install GoPhish

[GoPhish](https://getgophish.com/) i.e. an open source framework for creating phishing campaigns. It has many possibilities, including copying the website we want to spoof, copying the e-mail message we are going to send, the ability to attach a malicious file to our campaigns, and all this is summarized in user-friendly statistics (thanks to which we know how many messages have been sent, how many people opened the email, clicked on the link, and received information about the data provided on the website or new abuse reports).

So let's download gophish and unpack it into the `/opt` directory by typing: <br> 

```
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip -O /opt/gophish.zip

unzip /opt/gophish.zip -d /opt/gophish

cd /opt/gophish

chmod +x gophish
```
<br>
Don't launch GoPhish yet! The whole thing will run on localhost as a web application, so you won't be able to connect to the application through the console. Additionally, a password for the panel is generated when you first start it, so hold off for a moment!

To be able to manage GoPhish, it must redirect port 3333 (GoPhish's default port) from the VPS to our local machine also to port 3333. Importantly, GoPhish runs on the localhost, so we cannot connect to it like a standard web application. So let's create an SSH tunnel that will work according to our assumptions. In the new console window (you can close the old one), enter:
<br>

```
ssh -L 3333:127.0.0.1:3333 root@<ip> -p <port>
```
<br>

Now if you run GoPhish `./opt/gophish` in the console you will see your password for the admin panel (you will have to change it the first time you log in - the default login is admin)

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/gophish_password.png">
</p>

Now type https://127.0.0.1:3333 in your browser to see the GoPhish panel which looks like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/gophish_panel.png">
</p>

Change your password and look around the panel if you want. Once you're done, we'll move on to the next point.
<br>

### 6. Generating certificates for GoPhish

Connect to your VPS again using SSH (if you are connected you don't need to do this again). At this point we will generate TLS certificates for our phishing domain. As a word of explanation, GoPhish works in such a way that we do not have to have a "physically" phishing page anywhere, just the template of such a page in HTML is enough (believe me, it is enough). When starting a phishing campaign on the specified URL, GoPhish creates a phishing page "on the fly" from our template. The whole thing is great because no bot will be able to index our phishing website, and after the campaign ends, there will be no trace left on the website (which effectively protects us against detection of our goals and possible analysis of the website). We will use [certbot](https://certbot.eff.org/) to generate certificates. 

```
DOMAIN="haveibeenpwnd.pl" ### in " " enter your domain name
apt install snapd
service snapd start
snap install core
snap refresh core
apt-get remove certbot
snap install certbot --classic 
ln -s /snap/bin/certbot /usr/bin/certbot
certbot certonly --standalone -d "$DOMAIN"
mkdir /opt/gophish/ssl_keys
cp "/etc/letsencrypt/live/$DOMAIN/privkey.pem" /opt/gophish/ssl_keys/key.pem
cp "/etc/letsencrypt/live/$DOMAIN/fullchain.pem" /opt/gophish/ssl_keys/key.crt​
```
<br>

The certificate itself can also be purchased. However, this guide does not describe this procedure.

### 7. Further configuration of GoPhish

Let's start by editing `/opt/gophish/config.json` which contains the main GoPhish configuration. We need to add the generated keys from the previous point to the configuration. The whole thing should look like this:

```
{
        "admin_server": {
                "listen_url": "127.0.0.1:3333",
                "use_tls": true,
                "cert_path": "gophish_admin.crt",
                "key_path": "gophish_admin.key"
        },
        "phish_server": {
                "listen_url": "0.0.0.0:443",
                "use_tls": true,
                "cert_path": "/opt/gophish/ssl_keys/key.crt",
                "key_path": "/opt/gophish/ssl_keys/key.pem"
        },
        "db_name": "sqlite3",
        "db_path": "gophish.db",
        "migrations_prefix": "db/db_",
        "contact_address": "",
        "logging": {
                "filename": "",
                "level": ""
        }
}
```
<br>

The next step is to create a service through which we will be able to run, stop or restart GoPhish (the whole thing will run in the background). To do this, create the file `/etc/init.d/gophish` and then paste the following content into it:

```
#!/bin/bash
# /etc/init.d/gophish
# chkconfig: - 64 36
# description: stops/starts gophish application server
# processname:gophish

processName=Gophish
process=gophish
appDirectory=/opt/gophish
logfile=/var/log/gophish/gophish.log
errfile=/var/log/gophish/gophish.error

start() {
    echo 'Starting '${processName}'...'
    cd ${appDirectory}
    nohup ./$process >>$logfile 2>>$errfile &
    sleep 1
}

stop() {
    echo 'Stopping '${processName}'...'
    pid=$(/bin/pidof ${process})
    kill ${pid}
    sleep 1 
}

status() {
    pid=$(/bin/pidof ${process})
    if [["$pid" != ""| "$pid" != "" ]]; then
        echo ${processName}' is running...'
    else
        echo ${processName}' is not running...'
    fi
}

case $1 in
    start|stop|status) "$1" ;;
esac

```

<br>

Then execute the commands below:

```
mkdir /var/log/gophish
chmod +x /etc/init.d/gophish
update-rc.d gophish defaults
service gophish start
service gophish status ## You should have seen Active: active (running)
ss -l | grep "3333\|443" ## You should see that something is listening on port 3333
service gophish stop
```

<br>

If you did everything correctly, from now on you will be able to start/stop the GoPhish service using: `service gophish start/stop/restart`.

### 8. Postfix Configuration

It's time to install and then longer configure Postfix, i.e. the part of our infrastructure responsible for sending our phishing messages. It largely determines whether our emails will go to spam or will end up in the main folders of victims' mailboxes. So let's start with installing postfix:
<br>

```
apt-get install postfix
```

<br>

After installation, it's time to configure. So let's start by editing the `/etc/postfix/main.cf` file. Instead of `<domain>`, enter the name of your domain that you purchased in the first steps.
<br>
```
myhostname = <domain>
mydestination = $myhostname, <domain>, localhost.com, localhost
```
<br>

Additionally, make sure that the `/etc/hostname` and `/etc/mailname` files contain your domain name. If this doesn't happen, change it and restart your VPS.

At the end of the basic configuration, add an A record `mail.<domain>` to your DNS, pointing to the IP address of your VPS, and an MX record pointing to your mail server, i.e. `mail.<domain>`. If you have done everything correctly so far, you will be able to send the email. So let's install `mailutils` and send an email!
<br>
```
apt install mailutils
echo "Message" | mail -s "Topic" <mail> ## Instead of <mail>, enter the address to which you want to send the message
```
<br>

### 9. Further configuration of the mail server

However, before we move on to further configuration, we need to go through some additional theory. Remember how I wrote that our messages are rated and that the sum of these points determines whether our messages will go to spam or to main folders? One of the main criteria is to have **SPF**, **DKIM** and **DMARC** security. We will configure them later, but for now we need to find out what these security measures are.

**SPF** - It is basic and absolutely minimal security. It allows you to indicate which IP addresses can send emails from your domain.

**DMARC** - This additional protection was introduced in response to problems related to SPF. DKIM indicates whether a message sent from a given domain was actually sent by a real sender. 

**DKIM** - Setting up DMARC correctly ensures that no one can spoof your domain

If we already know that it is SPF, DMARC and DKIM, we can proceed to further configuration. To generate SPF, go to [https://www.spfwizard.net/](https://www.spfwizard.net/) and set the option according to the following example:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/spf.png">
</p>

After generating the value, create a new TXT record in your DNS. To set DMARC, just create a TXT record in DNS called `_dmarc.domain.pl` with the value `v=DMARC1; p=none`

To generate DKIM, we need to do more configuration, unfortunately if we want our Phishing to not be included in spam, this step is **necessary**.

So let's start by installing the necessary programs:

```
apt-get update
apt-get install opendkim opendkim-tools
```
<br>

The first thing we need to do after installation is to edit the `/etc/opendkim.conf` file, so let's enter:

```
nano /etc/opendkim.conf
```
<br>

And then set it as follows (of course, instead of `<domain>` enter your domain name):

```
Syslog			yes
SyslogSuccess	yes
LogWhy			yes

Canonicalization	relaxed/simple
Mode			sv

OversignHeaders		From

Domain			<domain>
Selector		mail
KeyFile		    /etc/opendkim/keys/<domain>/

UserID			opendkim:opendkim
UMask			002

Socket			inet:12301@localhost

PidFile			/var/run/opendkim/opendkim.pid

TrustAnchorFile		/usr/share/dns/root.key

AutoRestart             Yes
AutoRestartRate         10/1h


ExternalIgnoreList      refile:/etc/opendkim/TrustedHosts
InternalHosts           refile:/etc/opendkim/TrustedHosts
KeyTable                refile:/etc/opendkim/KeyTable
SigningTable            refile:/etc/opendkim/SigningTable

SignatureAlgorithm      rsa-sha256

```
<br>

Then let's edit `/etc/default/opendkim` and add to it:

```
SOCKET="inet:12301@localhost"
```
<br>

The next change we need to make is in the `/etc/postfix/main.cf` file, the entire file should look like this:

```
smtpd_banner = $myhostname ESMTP $mail_name (Debian/GNU)
biff = no

append_dot_mydomain = no

readme_directory = no

compatibility_level = 2

smtpd_tls_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
smtpd_tls_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
smtpd_tls_security_level=may

smtp_tls_CApath=/etc/ssl/certs
smtp_tls_security_level=may
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache


smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
myhostname = mail.<domain> 
myorigin = <domain> 
mydomain = <domain>
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
myorigin = /etc/mailname
mydestination = $myhostname, <domain>, localhost.pl, , localhost
relayhost = 

mynetworks = <ip> ## Instead of <ip>, enter the IP address of your VPS
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
inet_protocols = all
milter_protocol = 6
milter_default_action = accept
smtpd_milters = inet:localhost:12301
non_smtpd_milters = inet:localhost:12301

smtp_helo_name = $mydomain
relay_domains = $mydomain
```
<br>

Then execute the commands below:

```
mkdir /etc/opendkim
mkdir /etc/opendkim/keys
nano /etc/opendkim/TrustedHosts
```
<br>

In the `TrustedHosts` file, add:

```
127.0.0.1
localhost
192.168.0.1/24
<ip> Instead of <ip>, enter the IP address of your VPS

.<domain> ## Instead of `<domain>` enter your domain name
```
<br>

Additionally, create a `KeyTable` file:

<br>

```
nano /etc/opendkim/KeyTable
```
<br>

and paste the following content into it (of course, instead of `<domain>` enter your domain address):

```
mail._domainkey.<domain> <domain>:mail:/etc/opendkim/keys/<domain>/mail.private
```

<br>

Before we start generating our keys, we need to create the `SigningTable` file:

```
nano /etc/opendkim/SigningTable
```

<br>

and then complete the file with the following content (of course, instead of `<domain>` enter your domain address):

```
mail@<domain> mail._domainkey.<domain>
```
<br>

The e-mail address you provide in this file will be used to send our messages, so you can use e.g. noreply@domain.pl, support@domain.pl etc. You can change the address at any time.

### 10. Public and private key generation

It's time to generate keys, they are used to sign sent messages. The key that will be generated will have to be placed in the TXT record in our DNS. Without further ado, let's start generating keys:

```
cd /etc/opendkim/keys
mkdir <domain> ## You probably already know what to do with <domain> :)
cd <domain>
sudo opendkim-genkey -s mail -d <domain>
chown opendkim:opendkim mail.private
```
<br>

### 11. Adding a key to a DNS record

Open the `mail.txt` file, this is where your key is:

```
nano -$ mail.txt
```
<br>

The whole thing will look something like this:

```
mail._domainkey IN TXT "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC5N3lnvvrYgPCRSoqn+awTpE+iGYcKBPpo8HHbcFfCIIV10Hwo4PhCoGZSaKVHOjDm4yefKXhQjM7iKzEPuBatE7O47hAx1CJpNuIdLxhILSbEmbMxJrJAG0HZVn8z6EAoOHZNaPHmK2h4UUrjOG8zA5BHfzJf7tGwI+K619fFUwIDAQAB" ; ----- DKIM key mail for <domena>
```
<br>

All you need to do is add a TXT record to your DNS with the value you have in the file. Below you will find an example of what it should look like:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/dkim.png">
</p>

Now all you need to do is restart the appropriate services.

```
service postfix restart
service opendkim restart
```
<br>

To check if everything is set correctly, send an email to `check-auth@verifier.port25.com`. As feedback, we will receive information whether everything is configured correctly. So let's type:

```
echo "Message" | mail -s "Subject" check-auth@verifier.port25.com
```
<br>

You will receive a reply email after a few seconds. So let's wait a moment and type:

```
cat /var/mail/root ## If we operate from the root account
```
<br>

If everything is configured correctly in the email we should read:

```
==========================================================
Summary of Results
==========================================================
SPF check:          pass
DKIM check:         pass
```
<br>

### 12. Configuring Sending Profiles in GoPhish

Remember to set up a tunnel for GoPhish, otherwise you will not be able to connect to the panel.

```
ssh -L 3333:127.0.0.1:3333 root@<ip> -p <port>
```
<br>

Then go to https://127.0.0.1:3333 in your browser, log in, go to `Sending Profiles` and press the `New Profile` button. At this point it is worth explaining what Sending Profile is. This is the place where we define the profile settings from which our messages will be sent via Postfix, which we configured earlier. You can create many such profiles (when creating a campaign, we will be able to choose the profile from which we want to send messages).

GoPhish may have a problem if we send messages via port 25 (default port). So, before we start configuring Sending Profile, let's go to the console for a moment and uncomment a few lines in the `/etc/postfix/master.cf` file, so the beginning of the file should look like the following example:


```
smtp      inet  n       -       y       -       -       smtpd
submission inet n       -       y       -       -       smtpd
  -o syslog_name=postfix/submission
  -o smtpd_tls_security_level=encrypt
  -o smtpd_sasl_auth_enable=yes
```
<br>

Let's save the file and restart Postfix:

```
systemctl restart postfix
```
<br>

We can now return to configuring our Sending Profile according to the instructions below:

```
* Name: Enter a profile name here so that you can distinguish your profiles

* From: The address of the sender of our phishing attack - if you want only the email address without a name to appear in your inbox, enter e.g. support@domain.pl. If you want the sender's name to appear in the inbox instead of the email, enter e.g. Support<support@domain.pl> (the lack of spaces between the name and the email address is intentional)

* Host: Here we define the address of our email server. So enter mail.<domain>:587

* Ignore Certificate Errors: Mark

Add two headers:

* List-Unsubscribe with the value <mailto: unsubscribe@domain.com?subject=unsubscribe> - thanks to this header our messages will be rated better

* X-Mailer with a value, e.g. Thunderbird - without this header, the message headers will show information that the message was sent via GoPhish. Thanks to this header, we get rid of the problem
```
<br>

Ultimately it should look something like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/sending_profile.png">
</p>

<br>

If you want, you can send a test message to your mailbox at this point to see the result.

### 13. Defining the group to attack

To add groups that we will attack, select `Users&Groups` from the menu on the left. Here we need to define the group of people to whom we will send messages. If you think about it, you may come to the conclusion that it is good to have a list of our goals divided into groups, e.g. management, IT, HR, etc. In the case of spear phishing, for example, we may want to send a message to a specific group of people.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/group.png">
</p>


<br>

### 14. Creating a phishing page template

To create a template, go to `Landing Pages`. Here we prepare a website template that the victim will see after going to the provided link. The matter is so simple that if we want to create, for example, a copy of Facebook, just press the `New Page` button, provide the name of our Landing Page (so that we can distinguish templates in the future) and then press `Import Site` and enter the address of the page we want to copy. If we want to modify the page, we can edit the page code from the panel level (we can also create the page to which the person will be directed).

**NOTE** Remember to check `Capture Submitted Data` at the bottom and then check `Capture Passwords`, otherwise our phishing will not meet our assumptions. Additionally, in the `Redirect to:` field, you can enter the address of the website to which the victim should be redirected after entering his/her data. This may be, for example, the address of a real website so that the victim realizes that it is an error and then re-enters his credentials and logs in to his account.

**NOTE 2** If for some reason we want to place a copy of the website on our server running GoPhish, you must additionally install e.g. Apache or nginx. Additionally, in this case, you must configure SSL on your website and change the default port 443 to e.g. 8443, because the Phishing Server also works on port 443. Do not change the port of the Phishing Server under any circumstances. If you do this, the victim will receive a link that will look like this: `https://naszadomena.pl:8443`, which looks quite suspicious. Therefore, if you want to set up a website on a VPS, you need to change the ports in Apache or nginx (this guide does not include information on this subject).

After setting, everything should look like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/landing_page.png">
</p>


### 15. Creating a message template

Before we start our campaign, we need to take one more step. Go to `Email Templates` where you will be able to create email templates. Just like with the Landing Page, you will be able to import the original message. To do this, you need to go, for example, to the headers of a given message and then copy its HTML code and paste it into the appropriate place in GoPhish (New Template -> Import Email). Remember to leave the 'Change Links to Point to Landing Page' option checked, thanks to which all links from the real message will be replaced with the address of our landing page that you choose when creating the campaign. If you don't want to do this, uncheck this option now.

**NOTE** Leave the `Add Tracking Image` option checked, otherwise you will not be able to track the progress of the campaign, i.e. information about opening the message, clicking the link, etc.

Here you can also edit the message code or add malicious attachments. The whole thing should look something like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/email_template.png">
</p>

For more information on creating templates and landing pages, please refer to the GoPhish documentation available at: [https://getgophish.com/documentation/](https://getgophish.com/documentation/)

### 16. Creating your first Phishing campaign

**CONGRATULATIONS** After quite a long configuration, we can finally start our first phishing campaign! So let's go to `Campaigns` to get started!

This is where we create all phishing campaigns and soon we will see all statistics and entered passwords here. Without waiting any longer, press `New Campaign` and select your message template, landing page, sending profile and the group to which you want to send the messages. In the `URL` field, enter your domain address.

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/campaign.png">
</p>

If you are ready, press the appropriate `Launch` button to start sending. At this point, we have no choice but to wait until our victims see our message, visit the link provided and provide their data. For the purposes of this guide, I will simulate such a victim. Depending on the actions taken by victims, our dashboard will change. Additionally, after the victim enters their data on the phishing website, we will see them expanding the details for a specific person. The whole thing looks like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/notthehiddenwiki/NTHW/nthw/.github/notes/phishing/dashboard.png">
</p>

**TIP** Before sending the campaign, it is worth spending some time sending messages to your various email addresses (preferably to those that already have some history). What for? Despite all the configurations we have made, mailboxes still "do not trust" you as the sender. The more people (there may be one person with many mailboxes) open e-mails, click on links and do not simply ignore the e-mails or delete them immediately, the greater the reputation of the sender, which will also make our messages more trusted. Additionally, if it happens that your message ends up in spam, it is worth clicking that it is not SPAM and moving the message to the main folder.

<br><br>

**The article was written for educational purposes. I am not responsible for using the knowledge collected here in an unethical or illegal way.**