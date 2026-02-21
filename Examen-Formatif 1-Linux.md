## Examen Formatif 1 Linux — Questions à choix multiples (QCM)

### PARTIE 1 — Commandes de base & navigation (1–10)

**1) Quelle commande affiche le chemin du répertoire courant ?**
A) `whoami`
B) `pwd`
C) `path`
D) `where`

**2) Quelle commande liste les fichiers (y compris cachés) avec détails ?**
A) `ls -l`
B) `ls -a`
C) `ls -la`
D) `dir -a`

**3) Pour revenir au répertoire personnel (home), la commande la plus simple est :**
A) `cd /`
B) `cd`
C) `cd ..`
D) `cd ~root`

**4) Quel symbole représente le répertoire parent ?**
A) `.`
B) `..`
C) `~`
D) `*`

**5) Quelle commande crée un répertoire nommé `projet` ?**
A) `touch projet`
B) `mkfile projet`
C) `mkdir projet`
D) `create projet`

**6) Quelle commande copie `a.txt` vers `b.txt` ?**
A) `mv a.txt b.txt`
B) `cp a.txt b.txt`
C) `copy a.txt b.txt`
D) `dup a.txt b.txt`

**7) Quelle commande déplace `fichier` dans `backup/` ?**
A) `cp fichier backup/`
B) `mv fichier backup/`
C) `move fichier backup/`
D) `rename fichier backup/`

**8) Pour supprimer un répertoire vide `tmp`, on utilise :**
A) `rm tmp`
B) `rm -r tmp`
C) `rmdir tmp`
D) `del tmp`

**9) Quelle commande affiche les 10 dernières lignes d’un fichier `log.txt` ?**
A) `head log.txt`
B) `tail log.txt`
C) `less log.txt`
D) `cat -n log.txt`

**10) Quelle commande permet de lire un fichier page par page ?**
A) `cat`
B) `less`
C) `echo`
D) `nano -p`

---

### PARTIE 2 — Permissions & fichiers (11–20)

**11) Que signifie le premier caractère `d` dans `drwxr-xr-x` ?**
A) fichier exécutable
B) fichier caché
C) dossier (directory)
D) lien symbolique

**12) Quelle commande change les permissions d’un fichier ?**
A) `chown`
B) `chmod`
C) `chgrp`
D) `umask`

**13) `chmod 755 script.sh` donne :**
A) rwx pour tous
B) rwx pour propriétaire, r-x pour groupe, r-x pour autres
C) rw- pour propriétaire, r-- pour groupe, r-- pour autres
D) r-x pour propriétaire, rwx pour groupe, --- pour autres

**14) Quelle commande change le propriétaire d’un fichier ?**
A) `chmod`
B) `chown`
C) `chgrp`
D) `usermod`

**15) Quel est le rôle de `umask` ?**
A) supprimer les fichiers temporaires
B) définir les permissions par défaut à la création
C) chiffrer un fichier
D) afficher la taille des fichiers

**16) Quel type d’objet est `lrwxrwxrwx` ?**
A) fichier ordinaire
B) dossier
C) lien symbolique
D) périphérique bloc

**17) Quelle commande affiche la taille des fichiers dans un dossier en format lisible ?**
A) `df -h`
B) `du -h`
C) `free -h`
D) `ls -h`

**18) Quelle commande trouve un fichier nommé `notes.txt` à partir de `/home` ?**
A) `search /home notes.txt`
B) `find /home -name notes.txt`
C) `locate /home notes.txt`
D) `grep /home notes.txt`

**19) Quelle commande affiche le type d’un fichier ?**
A) `type fichier`
B) `file fichier`
C) `kind fichier`
D) `info fichier`

**20) Quelle commande compare deux fichiers texte ?**
A) `diff a.txt b.txt`
B) `cmp -h a.txt b.txt`
C) `compare a.txt b.txt`
D) `cut a.txt b.txt`

---

### PARTIE 3 — Redirections, pipes & recherche (21–30)

**21) Que fait `>` en shell ?**
A) ajoute à la fin
B) redirige la sortie en écrasant le fichier
C) redirige l’erreur uniquement
D) lit depuis un fichier

**22) Que fait `>>` ?**
A) écrase le fichier
B) ajoute à la fin du fichier
C) supprime un fichier
D) redirige l’entrée

**23) Quelle commande redirige uniquement les erreurs (stderr) vers `err.log` ?**
A) `cmd > err.log`
B) `cmd 2> err.log`
C) `cmd 1> err.log`
D) `cmd &> out.log` (uniquement erreurs)

**24) Que fait le pipe `|` ?**
A) exécute une commande en arrière-plan
B) envoie la sortie d’une commande vers l’entrée d’une autre
C) supprime les doublons
D) compresse la sortie

**25) Quelle commande cherche le mot `error` dans `app.log` ?**
A) `find error app.log`
B) `grep error app.log`
C) `search error app.log`
D) `locate error app.log`

**26) `grep -i` signifie :**
A) recherche récursive
B) insensible à la casse (maj/min)
C) affiche les numéros de ligne
D) inverse la sélection

**27) `grep -r "TODO" .` fait :**
A) recherche dans le fichier courant seulement
B) recherche récursive dans le dossier courant
C) remplace TODO
D) affiche uniquement les dossiers

**28) Quelle commande compte le nombre de lignes d’un fichier ?**
A) `wc -l fichier`
B) `count -l fichier`
C) `lines fichier`
D) `nl -c fichier`

**29) Quelle commande affiche uniquement la 1re colonne (séparateur espace) d’un fichier ?**
A) `cut -d ' ' -f1 fichier`
B) `awk -c1 fichier`
C) `head -c 1 fichier`
D) `split -1 fichier`

**30) Quelle commande affiche les 5 premières lignes ?**
A) `tail -n 5`
B) `head -n 5`
C) `less -n 5`
D) `cat -n 5`

---

### PARTIE 4 — Processus, système, réseau & services (31–40)

**31) Quelle commande affiche les processus en cours ?**
A) `ps`
B) `proc`
C) `jobs -a`
D) `top -l`

**32) Quelle commande affiche l’utilisation disque par partitions ?**
A) `du -h`
B) `df -h`
C) `free -h`
D) `lsblk -m`

**33) Quelle commande affiche l’utilisation mémoire ?**
A) `df`
B) `free -h`
C) `du`
D) `mount`

**34) Quel signal est envoyé par défaut avec `kill PID` ?**
A) SIGKILL (9)
B) SIGSTOP (19)
C) SIGTERM (15)
D) SIGHUP (1)

**35) Quelle commande montre les interfaces réseau et adresses IP (moderne) ?**
A) `ifconfig` uniquement
B) `ip a`
C) `netstat -i`
D) `route -n`

**36) Quelle commande teste la connectivité vers un hôte ?**
A) `ping`
B) `dig`
C) `scp`
D) `ssh-keygen`

**37) Avec systemd, quelle commande affiche l’état d’un service `ssh` ?**
A) `service ssh status`
B) `systemctl status ssh`
C) `initctl status ssh`
D) `chkconfig ssh`

**38) Quelle commande démarre un service `nginx` (systemd) ?**
A) `systemctl start nginx`
B) `systemctl enable nginx`
C) `service nginx enable`
D) `start nginx`

**39) Quelle commande active un service au démarrage (systemd) ?**
A) `systemctl run`
B) `systemctl enable`
C) `systemctl reload`
D) `systemctl init`

**40) Quelle commande affiche le journal systemd pour le service `ssh` ?**
A) `dmesg -u ssh`
B) `journalctl -u ssh`
C) `logctl ssh`
D) `syslog -u ssh`


