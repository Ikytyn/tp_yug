Partie A: 
1. Scann des ports pour l'IP cible:
$: nmap -p- --open 192.168.1.95
 Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-04-26 05:22 EDT
Nmap scan report for 192.168.1.95
Host is up (0.11s latency).
Not shown: 65498 closed tcp ports (reset), 34 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.5
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.7 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.52 ((Ubuntu))
MAC Address: E8:D0:FC:B1:81:21 (Liteon Technology)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 42.26 seconds

On voit les ports 21, 22 et 80 d'ouverts, je tape l'url de la machione avec le port 80 et je remarque que c'est un site wordpress qui tourne dessus.

2. Analyse du wordpress :
$: wpscan --url http://192.168.1.95 --enumerate p,t
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.25

       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[i] Updating the Database ...
[i] Update completed.

[+] URL: http://192.168.1.95/ [192.168.1.95]
[+] Started: Fri Apr 26 07:06:45 2024

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.52 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://192.168.1.95/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.1.95/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.1.95/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.1.95/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 6.5.2 identified (Latest, released on 2024-04-09).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.1.95/feed/, <generator>https://wordpress.org/?v=6.5.2</generator>
 |  - http://192.168.1.95/comments/feed/, <generator>https://wordpress.org/?v=6.5.2</generator>

[+] WordPress theme in use: twentytwentyfour
 | Location: http://192.168.1.95/wp-content/themes/twentytwentyfour/
 | Latest Version: 1.1 (up to date)
 | Last Updated: 2024-04-02T00:00:00.000Z
 | Readme: http://192.168.1.95/wp-content/themes/twentytwentyfour/readme.txt
 | Style URL: http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css
 | Style Name: Twenty Twenty-Four
 | Style URI: https://wordpress.org/themes/twentytwentyfour/
 | Description: Twenty Twenty-Four is designed to be flexible, versatile and applicable to any website. Its collecti...
 | Author: the WordPress team
 | Author URI: https://wordpress.org
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css, Match: 'Version: 1.1'

[+] Enumerating Most Popular Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Most Popular Themes (via Passive and Aggressive Methods)
 Checking Known Locations - Time: 00:00:04 <============> (400 / 400) 100.00% Time: 00:00:04
[+] Checking Theme Versions (via Passive and Aggressive Methods)

[i] Theme(s) Identified:

[+] twentytwentyfour
 | Location: http://192.168.1.95/wp-content/themes/twentytwentyfour/
 | Latest Version: 1.1 (up to date)
 | Last Updated: 2024-04-02T00:00:00.000Z
 | Readme: http://192.168.1.95/wp-content/themes/twentytwentyfour/readme.txt
 | Style URL: http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css
 | Style Name: Twenty Twenty-Four
 | Style URI: https://wordpress.org/themes/twentytwentyfour/
 | Description: Twenty Twenty-Four is designed to be flexible, versatile and applicable to any website. Its collecti...
 | Author: the WordPress team
 | Author URI: https://wordpress.org
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By:
 |  Urls In 404 Page (Passive Detection)
 |  Known Locations (Aggressive Detection)
 |   - http://192.168.1.95/wp-content/themes/twentytwentyfour/, status: 403
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css, Match: 'Version: 1.1'

[+] twentytwentythree
 | Location: http://192.168.1.95/wp-content/themes/twentytwentythree/
 | Latest Version: 1.4 (up to date)
 | Last Updated: 2024-04-02T00:00:00.000Z
 | Readme: http://192.168.1.95/wp-content/themes/twentytwentythree/readme.txt
 | Style URL: http://192.168.1.95/wp-content/themes/twentytwentythree/style.css
 | Style Name: Twenty Twenty-Three
 | Style URI: https://wordpress.org/themes/twentytwentythree
 | Description: Twenty Twenty-Three is designed to take advantage of the new design tools introduced in WordPress 6....
 | Author: the WordPress team
 | Author URI: https://wordpress.org
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentythree/, status: 403
 |
 | Version: 1.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentythree/style.css, Match: 'Version: 1.4'

[+] twentytwentytwo
 | Location: http://192.168.1.95/wp-content/themes/twentytwentytwo/
 | Latest Version: 1.7 (up to date)
 | Last Updated: 2024-04-02T00:00:00.000Z
 | Readme: http://192.168.1.95/wp-content/themes/twentytwentytwo/readme.txt
 | Style URL: http://192.168.1.95/wp-content/themes/twentytwentytwo/style.css
 | Style Name: Twenty Twenty-Two
 | Style URI: https://wordpress.org/themes/twentytwentytwo/
 | Description: Built on a solidly designed foundation, Twenty Twenty-Two embraces the idea that everyone deserves a...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentytwo/, status: 200
 |
 | Version: 1.7 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentytwo/style.css, Match: 'Version: 1.7'

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Apr 26 07:06:55 2024
[+] Requests Done: 456
[+] Cached Requests: 19
[+] Data Sent: 118.244 KB
[+] Data Received: 21.54 MB
[+] Memory used: 277.547 MB
[+] Elapsed time: 00:00:09


Voici un résumé:

- WordPress version 6.5.2 est utilisé, ce qui est la dernière version au moment de l'analyse.
- Le thème Twenty Twenty-Four est installé et activé.
- Aucun plugin n'a été trouvé.
- Des fichiers intéressants tels que robots.txt, readme.html et wp-cron.php sont présents sur le site.
- XML-RPC est activé sur le site.

Partie B : 
1. Test d'injection SQL 
$: sqlmap -u "http://192.168.1.95/wp-admin"
        ___
       __H__
 ___ ___[.]_____ ___ ___  {1.8.2#stable}
|_ -| . [.]     | .'| . |
|___|_  [']_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 08:46:08 /2024-04-26/

[08:46:08] [WARNING] you've provided target URL without any GET parameters (e.g. 'http://www.site.com/article.php?id=1') and without providing any POST parameters through option '--data'
do you want to try URI injections in the target URL itself? [Y/n/q] y
[08:46:20] [INFO] testing connection to the target URL
got a 301 redirect to 'http://192.168.1.95/wp-admin/'. Do you want to follow? [Y/n] y
you have not declared cookie(s), while server wants to set its own ('wordpress_test_cookie=WP%20Cookie%20check'). Do you want to use those [Y/n] y
[08:46:33] [INFO] checking if the target is protected by some kind of WAF/IPS
[08:46:33] [WARNING] reflective value(s) found and filtering out
[08:46:33] [INFO] testing if the target URL content is stable
[08:46:33] [WARNING] URI parameter '#1*' does not appear to be dynamic
[08:46:33] [WARNING] heuristic (basic) test shows that URI parameter '#1*' might not be injectable
[08:46:34] [INFO] testing for SQL injection on URI parameter '#1*'
[08:46:34] [INFO] testing 'AND boolean-based blind - WHERE or HAVING clause'
[08:46:37] [INFO] testing 'Boolean-based blind - Parameter replace (original value)'
[08:46:37] [INFO] testing 'MySQL >= 5.1 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (EXTRACTVALUE)'
[08:46:38] [INFO] testing 'PostgreSQL AND error-based - WHERE or HAVING clause'
[08:46:38] [INFO] testing 'Microsoft SQL Server/Sybase AND error-based - WHERE or HAVING clause (IN)'
[08:46:38] [INFO] testing 'Oracle AND error-based - WHERE or HAVING clause (XMLType)'
[08:46:39] [INFO] testing 'Generic inline queries'
[08:46:39] [INFO] testing 'PostgreSQL > 8.1 stacked queries (comment)'
[08:46:39] [INFO] testing 'Microsoft SQL Server/Sybase stacked queries (comment)'
[08:46:39] [INFO] testing 'Oracle stacked queries (DBMS_PIPE.RECEIVE_MESSAGE - comment)'
[08:46:40] [INFO] testing 'MySQL >= 5.0.12 AND time-based blind (query SLEEP)'
[08:46:40] [INFO] testing 'PostgreSQL > 8.1 AND time-based blind'
[08:46:40] [INFO] testing 'Microsoft SQL Server/Sybase time-based blind (IF)'
[08:46:41] [INFO] testing 'Oracle AND time-based blind'
it is recommended to perform only basic UNION tests if there is not at least one other (potential) technique found. Do you want to reduce the number of requests? [Y/n] n
[08:46:51] [INFO] testing 'Generic UNION query (NULL) - 1 to 10 columns'
[08:46:55] [WARNING] URI parameter '#1*' does not seem to be injectable
[08:46:55] [CRITICAL] all tested parameters do not appear to be injectable. Try to increase values for '--level'/'--risk' options if you wish to perform more tests. If you suspect that there is some kind of protection mechanism involved (e.g. WAF) maybe you could try to use option '--tamper' (e.g. '--tamper=space2comment') and/or switch '--random-agent'
[08:46:55] [WARNING] HTTP error codes detected during run:
404 (Not Found) - 108 times, 403 (Forbidden) - 2 times

[*] ending @ 08:46:55 /2024-04-26/

Selon la reponse de la commande il n'y a pas de faille apparante, mais cela ne signifie pas que mon site est 100% sécurié a l'injection SQL.

2. Pour faire du brut force il va dabor falloir trouver le nom de l'utilisateur admin 
 $: wpscan --url http://192.168.1.95 --enumerate u
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.25
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.1.95/ [192.168.1.95]
[+] Started: Fri Apr 26 09:10:13 2024

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.52 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://192.168.1.95/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.1.95/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.1.95/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.1.95/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 6.5.2 identified (Latest, released on 2024-04-09).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.1.95/feed/, <generator>https://wordpress.org/?v=6.5.2</generator>
 |  - http://192.168.1.95/comments/feed/, <generator>https://wordpress.org/?v=6.5.2</generator>

[+] WordPress theme in use: twentytwentyfour
 | Location: http://192.168.1.95/wp-content/themes/twentytwentyfour/
 | Latest Version: 1.1 (up to date)
 | Last Updated: 2024-04-02T00:00:00.000Z
 | Readme: http://192.168.1.95/wp-content/themes/twentytwentyfour/readme.txt
 | Style URL: http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css
 | Style Name: Twenty Twenty-Four
 | Style URI: https://wordpress.org/themes/twentytwentyfour/
 | Description: Twenty Twenty-Four is designed to be flexible, versatile and applicable to any website. Its collecti...
 | Author: the WordPress team
 | Author URI: https://wordpress.org
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.1 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.1.95/wp-content/themes/twentytwentyfour/style.css, Match: 'Version: 1.1'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <==============> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] toto
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Wp Json Api (Aggressive Detection)
 |   - http://192.168.1.95/wp-json/wp/v2/users/?per_page=100&page=1
 |  Rss Generator (Aggressive Detection)
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Apr 26 09:10:17 2024
[+] Requests Done: 50
[+] Cached Requests: 8
[+] Data Sent: 12.653 KB
[+] Data Received: 584.368 KB
[+] Memory used: 201.734 MB
[+] Elapsed time: 00:00:04


L'utilisateur toto a été trouver grace a cette commande, je vais donc utiliser hydra pour essayer de cracker son mot de passe.

J'ai donc utiliser une liste de mot de passe avec les 100 mots de passe les plus utilisé + le mot de passe du compte admin de wordpress a l'intéerieur et j'ai executé cette commande :

$: echo -n "P@ssw0rd" | md5sum | awk '{print "toto:" $1}' > hash.txt

Pour creer un hash manuellement

Ensuite j'ai utilisé cette commande pour essayer de cracker le mot de passe

$: john --wordlist=/usr/share/wordlists/personal.lst hash.txt
Created directory: /root/.john
Warning: detected hash type "LM", but the string is also recognized as "dynamic=md5($p)"
Use the "--format=dynamic=md5($p)" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "HAVAL-128-4"
Use the "--format=HAVAL-128-4" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "MD2"
Use the "--format=MD2" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "mdc2"
Use the "--format=mdc2" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "mscash"
Use the "--format=mscash" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "mscash2"
Use the "--format=mscash2" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "NT"
Use the "--format=NT" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "Raw-MD4"
Use the "--format=Raw-MD4" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "Raw-MD5"
Use the "--format=Raw-MD5" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "Raw-MD5u"
Use the "--format=Raw-MD5u" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "Raw-SHA1-AxCrypt"
Use the "--format=Raw-SHA1-AxCrypt" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "ripemd-128"
Use the "--format=ripemd-128" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "Snefru-128"
Use the "--format=Snefru-128" option to force loading these as that type instead
Warning: detected hash type "LM", but the string is also recognized as "ZipMonster"
Use the "--format=ZipMonster" option to force loading these as that type instead
Using default input encoding: UTF-8
Using default target encoding: CP850
Loaded 2 password hashes with no different salts (LM [DES 128/128 AVX])
Warning: poor OpenMP scalability for this hash type, consider --fork=4
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 100 candidates left, minimum 512 needed for performance.
0g 0:00:00:00 DONE (2024-04-26 09:52) 0g/s 10000p/s 10000c/s 20000C/s PASSWOR..ZACH
Session completed

J'obtiens comme information que le formaty du mot de passe est en md5, j'ajuste donc ma commande

$: john --format=raw-md5 --wordlist=/usr/share/wordlists/personal.lst hash.txt

Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
P@ssw0rd         (toto)
1g 0:00:00:00 DONE (2024-04-26 09:53) 100.0g/s 10000p/s 10000c/s 10000C/s password..zach
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed.

J'obtiens le mot de passe de la session administrateur du wordpress.

Partie C :
1.	Sécurité WordPress :
-	Se connecter a WordPress en tant qu'administrateur.
-	Accédez au menu "Extensions" et cliquez sur "Ajouter une extensions".
-	Recherchez le plugin "Wordfence Security" et installez-le.
-	Activez le plugin et accédez à la page de configuration.
-	Configurez les paramètres de sécurité recommandés par Wordfence, tels que la protection -contre les forces brutes, le blocage d'adresses IP, etc.
-	Mettez en place des politiques de gestion des mises à jour pour assurer la sécurité des thèmes et plugins. Vous pouvez configurer des mises à jour automatiques pour les plugins et les thèmes, ou les mettre à jour manuellement régulièrement.

A partir d’ici, en activant les paramètre recommander j’ai cassé mon site 
 
A partir d’ici je dirais seulement ce que je comptais faire pour mettre en place

2.	Politiques de Mot de Passe :
-	Appliquez des politiques de mot de passe conformes aux recommandations de l'ANSSI. Par exemple, exigez des mots de passe complexes avec au moins 12 caractères, incluant des lettres majuscules et minuscules, des chiffres et des caractères spéciaux.
-	Mettez en place une politique de renouvellement régulier des mots de passe, par exemple tous les 90 jours.
-	Limitez le nombre de tentatives de connexion infructueuses pour éviter les attaques par force brute.

3.	Sauvegarde et Restauration :
Nous avons déjà mis en place un script qui fait une sauvegarde du dossier /var/www/wordpress, la base de données sql et qui va chiffrer ça avec une clef générer via openssl. Le tout est envoyé via sftp a un server Ubuntu de backup, voici le script :
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

import shutil
import subprocess
import os
import datetime
import paramiko
import random
import string

# Répertoire source contenant les données à sauvegarder
source_dir = '/var/www/wordpress/'

# Répertoire de sauvegarde où seront stockées les sauvegardes
backup_dir = '/home/toto/'

# Nom de base de l'archive de sauvegarde
backup_base_name = 'wordpress_backup_' + datetime.datetime.now().strftime('%Y-%m-%d')

# Fonction pour générer une clé de chiffrement aléatoire
def generate_encryption_key():
    return ''.join(random.choices(string.ascii_letters + string.digits, k=16))

# Génération de la clé de chiffrement
encryption_key = generate_encryption_key()

# Chemin vers le fichier contenant la clé de chiffrement
encryption_key_file = os.path.join(backup_dir, 'encryption_key.txt')

# Écriture de la clé de chiffrement dans un fichier
with open(encryption_key_file, 'w') as key_file:
    key_file.write(encryption_key)

print("Encryption key generated successfully")

# Sauvegarde de la base de données MySQL dans un fichier SQL
mysql_user = 'wordpressuser'
mysql_password = 'P@ssw0rd'
mysql_database = 'wordpress'

mysql_backup_file = os.path.join(backup_dir, 'mysql_backup.sql')

try:
    mysql_dump_command = f"mysqldump -u {mysql_user} -p{mysql_password} {mysql_database} > {mysql_backup_file}"
    subprocess.call(mysql_dump_command, shell=True)
    print("MySQL backup completed successfully")
except Exception as e:
    print("Error occurred while backing up MySQL:", e)

# Copie du contenu du répertoire FTP dans le répertoire de sauvegarde
try:
    shutil.copytree(source_dir, os.path.join(backup_dir, 'www'))
    print("Website directory copied successfully")
except Exception as e:
    print("Error occurred while copying website directory:", e)

# Création de l'archive contenant la sauvegarde MySQL et le contenu FTP
backup_name = f"{backup_base_name}_{datetime.datetime.now().strftime('%H-%M-%S')}.tar.gz"

try:
    shutil.make_archive(os.path.join(backup_dir, backup_name.split('.')[0]), 'gztar', backup_dir)
    print("Archive created successfully")
except Exception as e:
    print("Error occurred while creating archive:", e)

# Chiffrement de l'archive avec OpenSSL
encrypted_backup_file = os.path.join(backup_dir, f"encrypted_{backup_name}")

try:
    openssl_encrypt_command = f"openssl enc -aes-256-cbc -salt -in {backup_name} -out {encrypted_backup_file} -pass file:{encryption_key_file}"
    subprocess.call(openssl_encrypt_command, shell=True)
    print("Encryption completed successfully")
except Exception as e:
    print("Error occurred while encrypting backup file:", e)

# Détails de connexion SFTP pour le serveur distant
sftp_host = '192.168.1.22'
sftp_port = 22
sftp_username = 'toto'
sftp_password = 'toto'

# Connexion au serveur SFTP et envoi de l'archive chiffrée et de la clé de chiffrement
try:
    transport = paramiko.Transport((sftp_host, sftp_port))
    transport.connect(username=sftp_username, password=sftp_password)
    sftp = paramiko.SFTPClient.from_transport(transport)
    print("Connected to SFTP server")

    sftp.put(encrypted_backup_file, os.path.basename(encrypted_backup_file))
    sftp.put(encryption_key_file, os.path.basename(encryption_key_file))
    print("Backup and encryption key uploaded successfully")

    sftp.close()
    transport.close()
except paramiko.AuthenticationException:
    print("Authentication failed. Please check your SFTP credentials.")
except Exception as e:
    print("Error occurred during SFTP transfer:", e)
finally:
    # Nettoyage : suppression des fichiers temporaires et des répertoires
    os.remove(encryption_key_file)
    os.remove(encrypted_backup_file)
    os.remove(mysql_backup_file)
    shutil.rmtree(os.path.join(backup_dir, 'www'))
    print("Temporary files and directories deleted successfully")
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
Il suffit d ’exécuter le script via le crontab et on a mis en place une sauvegarde sécuriser sur un serveur distant.


