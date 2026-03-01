<h2>Examen Formatif 1 Linux — Questions à choix multiples (QCM)</h2>

<h3>PARTIE 1 — Commandes de base &amp; navigation (1–10)</h3>

<details> <summary> PARTIE 1 — Commandes de base &amp; navigation (1–10)  </summary></details>
<p><strong>1) Quelle commande affiche le chemin du répertoire courant ?</strong><br>
A) <code>whoami</code><br>
B) <code>pwd</code><br>
C) <code>path</code><br>
D) <code>where</code>
</p>

<p><strong>2) Quelle commande liste les fichiers (y compris cachés) avec détails ?</strong><br>
A) <code>ls -l</code><br>
B) <code>ls -a</code><br>
C) <code>ls -la</code><br>
D) <code>dir -a</code>
</p>

<p><strong>3) Pour revenir au répertoire personnel (home), la commande la plus simple est :</strong><br>
A) <code>cd /</code><br>
B) <code>cd</code><br>
C) <code>cd ..</code><br>
D) <code>cd ~root</code>
</p>

<p><strong>4) Quel symbole représente le répertoire parent ?</strong><br>
A) <code>.</code><br>
B) <code>..</code><br>
C) <code>~</code><br>
D) <code>*</code>
</p>

<p><strong>5) Quelle commande crée un répertoire nommé <code>projet</code> ?</strong><br>
A) <code>touch projet</code><br>
B) <code>mkfile projet</code><br>
C) <code>mkdir projet</code><br>
D) <code>create projet</code>
</p>

<p><strong>6) Quelle commande copie <code>a.txt</code> vers <code>b.txt</code> ?</strong><br>
A) <code>mv a.txt b.txt</code><br>
B) <code>cp a.txt b.txt</code><br>
C) <code>copy a.txt b.txt</code><br>
D) <code>dup a.txt b.txt</code>
</p>

<p><strong>7) Quelle commande déplace <code>fichier</code> dans <code>backup/</code> ?</strong><br>
A) <code>cp fichier backup/</code><br>
B) <code>mv fichier backup/</code><br>
C) <code>move fichier backup/</code><br>
D) <code>rename fichier backup/</code>
</p>

<p><strong>8) Pour supprimer un répertoire vide <code>tmp</code>, on utilise :</strong><br>
A) <code>rm tmp</code><br>
B) <code>rm -r tmp</code><br>
C) <code>rmdir tmp</code><br>
D) <code>del tmp</code>
</p>

<p><strong>9) Quelle commande affiche les 10 dernières lignes d’un fichier <code>log.txt</code> ?</strong><br>
A) <code>head log.txt</code><br>
B) <code>tail log.txt</code><br>
C) <code>less log.txt</code><br>
D) <code>cat -n log.txt</code>
</p>

<p><strong>10) Quelle commande permet de lire un fichier page par page ?</strong><br>
A) <code>cat</code><br>
B) <code>less</code><br>
C) <code>echo</code><br>
D) <code>nano -p</code>
</p>

<hr>

<h3>PARTIE 2 — Permissions &amp; fichiers (11–20)</h3>

<p><strong>11) Que signifie le premier caractère <code>d</code> dans <code>drwxr-xr-x</code> ?</strong><br>
A) fichier exécutable<br>
B) fichier caché<br>
C) dossier (directory)<br>
D) lien symbolique
</p>

<p><strong>12) Quelle commande change les permissions d’un fichier ?</strong><br>
A) <code>chown</code><br>
B) <code>chmod</code><br>
C) <code>chgrp</code><br>
D) <code>umask</code>
</p>

<p><strong>13) <code>chmod 755 script.sh</code> donne :</strong><br>
A) rwx pour tous<br>
B) rwx pour propriétaire, r-x pour groupe, r-x pour autres<br>
C) rw- pour propriétaire, r-- pour groupe, r-- pour autres<br>
D) r-x pour propriétaire, rwx pour groupe, --- pour autres
</p>

<p><strong>14) Quelle commande change le propriétaire d’un fichier ?</strong><br>
A) <code>chmod</code><br>
B) <code>chown</code><br>
C) <code>chgrp</code><br>
D) <code>usermod</code>
</p>

<p><strong>15) Quel est le rôle de <code>umask</code> ?</strong><br>
A) supprimer les fichiers temporaires<br>
B) définir les permissions par défaut à la création<br>
C) chiffrer un fichier<br>
D) afficher la taille des fichiers
</p>

<p><strong>16) Quel type d’objet est <code>lrwxrwxrwx</code> ?</strong><br>
A) fichier ordinaire<br>
B) dossier<br>
C) lien symbolique<br>
D) périphérique bloc
</p>

<p><strong>17) Quelle commande affiche la taille des fichiers dans un dossier en format lisible ?</strong><br>
A) <code>df -h</code><br>
B) <code>du -h</code><br>
C) <code>free -h</code><br>
D) <code>ls -h</code>
</p>

<p><strong>18) Quelle commande trouve un fichier nommé <code>notes.txt</code> à partir de <code>/home</code> ?</strong><br>
A) <code>search /home notes.txt</code><br>
B) <code>find /home -name notes.txt</code><br>
C) <code>locate /home notes.txt</code><br>
D) <code>grep /home notes.txt</code>
</p>

<p><strong>19) Quelle commande affiche le type d’un fichier ?</strong><br>
A) <code>type fichier</code><br>
B) <code>file fichier</code><br>
C) <code>kind fichier</code><br>
D) <code>info fichier</code>
</p>

<p><strong>20) Quelle commande compare deux fichiers texte ?</strong><br>
A) <code>diff a.txt b.txt</code><br>
B) <code>cmp -h a.txt b.txt</code><br>
C) <code>compare a.txt b.txt</code><br>
D) <code>cut a.txt b.txt</code>
</p>

<hr>

<h3>PARTIE 3 — Redirections, pipes &amp; recherche (21–30)</h3>

<p><strong>21) Que fait <code>&gt;</code> en shell ?</strong><br>
A) ajoute à la fin<br>
B) redirige la sortie en écrasant le fichier<br>
C) redirige l’erreur uniquement<br>
D) lit depuis un fichier
</p>

<p><strong>22) Que fait <code>&gt;&gt;</code> ?</strong><br>
A) écrase le fichier<br>
B) ajoute à la fin du fichier<br>
C) supprime un fichier<br>
D) redirige l’entrée
</p>

<p><strong>23) Quelle commande redirige uniquement les erreurs (stderr) vers <code>err.log</code> ?</strong><br>
A) <code>cmd &gt; err.log</code><br>
B) <code>cmd 2&gt; err.log</code><br>
C) <code>cmd 1&gt; err.log</code><br>
D) <code>cmd &amp;&gt; out.log</code> (redirige stdout+stderr)
</p>

<p><strong>24) Que fait le pipe <code>|</code> ?</strong><br>
A) exécute une commande en arrière-plan<br>
B) envoie la sortie d’une commande vers l’entrée d’une autre<br>
C) supprime les doublons<br>
D) compresse la sortie
</p>

<p><strong>25) Quelle commande cherche le mot <code>error</code> dans <code>app.log</code> ?</strong><br>
A) <code>find error app.log</code><br>
B) <code>grep error app.log</code><br>
C) <code>search error app.log</code><br>
D) <code>locate error app.log</code>
</p>

<p><strong>26) <code>grep -i</code> signifie :</strong><br>
A) recherche récursive<br>
B) insensible à la casse (maj/min)<br>
C) affiche les numéros de ligne<br>
D) inverse la sélection
</p>

<p><strong>27) <code>grep -r "TODO" .</code> fait :</strong><br>
A) recherche dans le fichier courant seulement<br>
B) recherche récursive dans le dossier courant<br>
C) remplace TODO<br>
D) affiche uniquement les dossiers
</p>

<p><strong>28) Quelle commande compte le nombre de lignes d’un fichier ?</strong><br>
A) <code>wc -l fichier</code><br>
B) <code>count -l fichier</code><br>
C) <code>lines fichier</code><br>
D) <code>nl -c fichier</code>
</p>

<p><strong>29) Quelle commande affiche uniquement la 1re colonne (séparateur espace) d’un fichier ?</strong><br>
A) <code>cut -d ' ' -f1 fichier</code><br>
B) <code>awk -c1 fichier</code><br>
C) <code>head -c 1 fichier</code><br>
D) <code>split -1 fichier</code>
</p>

<p><strong>30) Quelle commande affiche les 5 premières lignes ?</strong><br>
A) <code>tail -n 5</code><br>
B) <code>head -n 5</code><br>
C) <code>less -n 5</code><br>
D) <code>cat -n 5</code>
</p>

<hr>

<h3>PARTIE 4 — Processus, système, réseau &amp; services (31–40)</h3>

<p><strong>31) Quelle commande affiche les processus en cours ?</strong><br>
A) <code>ps</code><br>
B) <code>proc</code><br>
C) <code>jobs -a</code><br>
D) <code>top -l</code>
</p>

<p><strong>32) Quelle commande affiche l’utilisation disque par partitions ?</strong><br>
A) <code>du -h</code><br>
B) <code>df -h</code><br>
C) <code>free -h</code><br>
D) <code>lsblk -m</code>
</p>

<p><strong>33) Quelle commande affiche l’utilisation mémoire ?</strong><br>
A) <code>df</code><br>
B) <code>free -h</code><br>
C) <code>du</code><br>
D) <code>mount</code>
</p>

<p><strong>34) Quel signal est envoyé par défaut avec <code>kill PID</code> ?</strong><br>
A) SIGKILL (9)<br>
B) SIGSTOP (19)<br>
C) SIGTERM (15)<br>
D) SIGHUP (1)
</p>

<p><strong>35) Quelle commande montre les interfaces réseau et adresses IP (moderne) ?</strong><br>
A) <code>ifconfig</code> uniquement<br>
B) <code>ip a</code><br>
C) <code>netstat -i</code><br>
D) <code>route -n</code>
</p>

<p><strong>36) Quelle commande teste la connectivité vers un hôte ?</strong><br>
A) <code>ping</code><br>
B) <code>dig</code><br>
C) <code>scp</code><br>
D) <code>ssh-keygen</code>
</p>

<p><strong>37) Avec systemd, quelle commande affiche l’état d’un service <code>ssh</code> ?</strong><br>
A) <code>service ssh status</code><br>
B) <code>systemctl status ssh</code><br>
C) <code>initctl status ssh</code><br>
D) <code>chkconfig ssh</code>
</p>

<p><strong>38) Quelle commande démarre un service <code>nginx</code> (systemd) ?</strong><br>
A) <code>systemctl start nginx</code><br>
B) <code>systemctl enable nginx</code><br>
C) <code>service nginx enable</code><br>
D) <code>start nginx</code>
</p>

<p><strong>39) Quelle commande active un service au démarrage (systemd) ?</strong><br>
A) <code>systemctl run</code><br>
B) <code>systemctl enable</code><br>
C) <code>systemctl reload</code><br>
D) <code>systemctl init</code>
</p>

<p><strong>40) Quelle commande affiche le journal systemd pour le service <code>ssh</code> ?</strong><br>
A) <code>dmesg -u ssh</code><br>
B) <code>journalctl -u ssh</code><br>
C) <code>logctl ssh</code><br>
D) <code>syslog -u ssh</code>
</p>
