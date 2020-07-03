# avid-ansible
Ansible role for Avid Media Composer editing sofware deployement on Windows.
Based from this article : [https://blog.pntgn.io/blog/automate-avid-mediacomposer-installation/](https://blog.pntgn.io/blog/automate-avid-mediacomposer-installation/)

It has been tested with 8.6.5 and 18.12.3 version of Avid Media Composer editing software.

This role can be use to install AvidMediaComposer with vcredist, Pace drive, Sentinel driver and associated certificates.

## Requirements & Configuration
### Download Avid Media Composer
First, you'll need to download Avid Media Composer composer software. You can do this by connectiong to your account at [https://my.avid.com/account](https://my.avid.com/account)
Then go to the download center and chose the desired version you want to install.
This role has been tested with 8.6.5 and 18.12.3 versions. If you want to use another version, you'll have to add some variables, and maybe make some adjustements.

### Recover Avid and Pace certificates
The first time (or for every new version of Avid), you will need to recover Avid and Pace certificates manually.
Here is how you can get them:

- Install the AVID version you want manually.
- Open the certfificates manager (you can type "Manage User Certificates" on windows search bar. Also available from the control panel).
- In the 'TrustedPublishers/Certficiates', you'll find 2 certificates ('Pace' and 'Avid'). Just export them into 'DER' format.

### Configuration of SMB share
This playbook has been designed to work with an existing samba share in your network acting like a repository. ansible_role will copy required files from that directory.
You can configure the path to your SMB share and user login in 'avid_playbook.yml' file.

Into that directory, you'll need to have, for each version of Avid Media Composer, a folder called **AvidMediaComposer_$version** (where '$version' is replaced by the full version of AvidMediaComposer. for example: AvidMediaComposer_2018_12.3).
Inside that folder, you'll need to put:
- the downloaded .zip file from Avid website (cf "Download Avid Media Composer" section)
- a folder called **CertificatesTrustedPublisher** that contain the two certificates previously downloaded (cf "Recover Avid and Pace certificates" section)

### hosts.yml and roles/avid/vars/mail.yml files
Don't forget to use your own **hosts.yml** file and modify the 'hosts' variable into **avid_playbook.yml** before launching the playbook.
Also, remember that you'll have to configure roles/avid/vars/main.yml !

