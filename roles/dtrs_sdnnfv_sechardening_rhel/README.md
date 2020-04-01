# RedHat Enterprise Linux security hardening for DTRS SDN/NFV projects
Ce playbook a pour objectif de renforce la sécurité système des infrastructures de virtualisation.
Il a été testé avec RHEL 7.6 et RHOSP 13.

Ce playbook est basé sur automconfig, merci ;)

## Actions effectuées ##
### tag: ANSSI_linux_R32 ###
Configure /etc/login.def pour renforcer le hashage des mots de passe locaux conformément à la recommandations R32 du document DAT-NT-28 de l'ANSSI.
### tag: auditd_configuration ###
Configure auditd pour surveiller les actions effectuées sur le système.
Les actions surveillées sont:
- chargement ou déchargement d'un module noyau
- événements de type login/logout
- modification des informations de date ou de temps
- modification des droits des fichiers
- suppression de répertoires ou fichiers
- utilisation de commandes privilégiées
- tentatives d'accès à des fichiers non autorisés
- modification des fichiers /etc/passwd, /etc/shadow, /etc/group
- modification de la configuration réseau
- modification des règles sudo et SELinux
### tag: bluetooth ###
Désactive la prise en charge du Bluetooth
### tag: coredumps ###
Désactive la génération de core dumps
### tag: IP_configuration ###
Désactive la prise en charge d'IPv6.
Pour IPv4, configure les paramètres suivants :
- net.ipv4.icmp_echo_ignore_broadcasts => '1'
- net.ipv4.tcp_syncookies => '1'
- net.ipv4.conf.all.accept_redirects => '0'
- net.ipv4.icmp_ignore_bogus_error_responses => '1'
- net.ipv4.conf.default.log_martians => '1'
- net.ipv4.conf.all.log_martians => '1'
- net.ipv4.conf.default.secure_redirects => '0'
- net.ipv4.conf.all.secure_redirects => '0'
- net.ipv4.conf.default.accept_redirects => '0'
Désactive la prise en charge des protocoles DCCP et SCTP.
### tag: local_users_password ###
Mets en place du contrôle de complexité des mots de passe des utilisateurs locaux en suivant les règles suivantes :
- Password must contain at least one upper-case character
- Password must contain at least one lower-case character
- Password must contain at least one numeric character
- Password must contain at least one special character
- Password must have at least eight characters changed
- Password must have at least four character classes changed
- Password must have at most three characters repeated consecutively
- Password must have at most four characters in the same character class repeated consecutively
- Password must be a minimum of 15 characters in length
Liste les utilisateurs ayant un uid 0.
Mets en place la désactivation temporaire des utilisateurs suite à 5 échecs de mot de passe.
Empêche la connexion avec un utilisteur sans mot de passe de défini.
### tag: RS404-2100 ###
Mets en place la règle 2100 de la ROS404 : "Limit root access using console on tty1"
### tag: RS404-2200 ###
Mets en place la règle 2200 de la ROS404 : "Modify umask of root and users"
### tag: rsyslog_remote_loghost ###
Configure l'envoi des logs au serveur défini dans la variable "rsyslog_remote_loghost_address".
### tag: services_disable ###
Désactive les services:
- 'rpcbind'
- 'xinetd'
### tag: uncommon_filesystems ###
Désactive la prise en charge des systèmes de fichiers suivants:
- 'freevxfs'
- 'cramfs'
- 'squashfs'
- 'hfsplus'
- 'jffs2'
- 'hfs'
- 'udf'
### tag: usb-storage ###
Désactive le support des support de stockages USB
### tag: yum_gpgcheck ###
Active l'utilisation de gpgcheck pour vérifier les signatures des paquets logiciels.
### tag: AIDE_configuration ###
Pour vérifier l'intégrité du système, installe AIDE si il n'est pas présent et l'active.
Attention: la liste des fichiers à exclure n'est pas finalisée