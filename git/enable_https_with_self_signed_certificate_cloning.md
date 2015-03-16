# Enable https cloning with self-signed certificate

*tested on ubuntu 14.04*

When you want to clone a repo on a private server with a self-signed
certificate, you get this annoying error message:

    $ git clone https://gitlab.mydomain.com/user/repo.git
    Clonage dans 'repo'...
    fatal: unable to access 'https://gitlab.mydomain.com/user/repo.git/': server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile: none

First get the server private certificate and put it in `/usr/local/share/ca-certificates`

    $ SERVER=git.mydomain.com
    $ echo -n | openssl s_client -showcerts -connect $SERVER:443 2>/dev/null \
       | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'                \
       | sudo tee -a /usr/local/share/ca-certificates/$SERVER.crt

Then run `update-certificates` to include this cert in the local database:

    $ sudo update-certificates
    1 added, 0 removed; done.
    Running hooks in /etc/ca-certificates/update.d....
    Adding debian:gitlab.univ-lille3.fr.pem
    done.
    done.

You can now clone the repo:

    $ git clone https://gitlab.mydomain.com/user/repo.git
    Clonage dans 'repo'...
    remote: Counting objects: 144, done.
    remote: Compressing objects: 100% (142/142), done.
    remote: Total 144 (delta 43), reused 0 (delta 0)
    Réception d'objets: 100% (144/144), 7.93 MiB | 9.48 MiB/s, done.
    Résolution des deltas: 100% (43/43), done.
    Vérification de la connectivité... fait.

*Courtesy of @lwafflard*
