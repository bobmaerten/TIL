# Check for needed service restarts

After a system upgrade, where some libraries have been fixed, some services must be restarted.
The `checkrestart` command from the *debian-goodies* package make this check for you.

## Example

After the [GHOST](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-0235) security breach fixup, a lot of libc libraries have been patched. Here is the fresh-after-upgrade `checkrestart` result :

    # checkrestart
    Found 20 processes using old versions of upgraded files
    (13 distinct programs)
    (11 distinct packages)

    Of these, 8 seem to contain init scripts which can be used to restart them:
    The following packages seem to have init scripts that could be used
    to restart them:
    nfs-common:
    	2019	/usr/sbin/rpc.idmapd
    	2005	/sbin/rpc.statd
    rpcbind:
    	1974	/sbin/rpcbind
    acpid:
    	2496	/usr/sbin/acpid
    udev:
    	451	/sbin/udevd
    	452	/sbin/udevd
    	336	/sbin/udevd
    cron:
    	2679	/usr/sbin/cron
    at:
    	2553	/usr/sbin/atd
    rsyslog:
    	2409	/usr/sbin/rsyslogd
    nagios-nrpe-server:
    	2727	/usr/sbin/nrpe

    These are the init scripts:
    service nfs-common restart
    service rpcbind restart
    service acpid restart
    service udev-mtab restart
    service udev restart
    service cron restart
    service atd restart
    service rsyslog restart
    service nagios-nrpe-server restart

    These processes do not seem to have an associated init script to restart them:
    openssh-client:
    	3408	/usr/bin/ssh-agent
    perl-base:
    	2359	/usr/bin/perl

Note that if you do not want to restart your server (IMHO: the best way to be sure), the program gives you the list of services to be restarted. Neat!
