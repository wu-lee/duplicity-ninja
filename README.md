Duplicity Ninja
---------------

# NAME

duplicity-ninja - run common duplicity commands in the context of backupninja 

# SYNOPSIS

      $ duplicity-ninja -h
    Usage:
	duplicity-ninja <cmd>

    Where <cmd> can be:

	restore [-t <time>] [-f <file-to-restore>] [common-opts]
	list-current-files [-t <when>]
	collection-status
	remove-all-but-n-full -N <count> [-F]
	remove-older-than [-t <when>] [-F]
	cleanup [-F]
	verify [-f <file-to-verify>]
	help


    Options are:

	-F    force, actually delete stuff rather than report what would be done
	-N <count>  supplies the number of full backups to remove
	-f <path>   supplies a file or directory to verify (recursively)
	-C <path>   overrides the default backupninja.conf file: /etc/backupninja.conf
	-c <path>   overrides the default duplicity backup config: /etc/backup.d/50.backup.dup
	-t <when>   overrides the default time, 'now'
	-d <path>   overrides the default restore destination: /var/tmp/duplicity-restores
	-n          just print the command which would be executed
	-h          print this help (same as the help / no command)


An example of running listing the backups (actual key IDs redacted):
   
      $ sudo duplicity-ninja collection-status
    Data will be encrypted with the GnuPG key F00DFACE.
    Data will be signed will the GnuPG key F00DFACE.
    Using /tmp as TMPDIR
    duplicity collection-status --encrypt-key F00DFACE --sign-key F00DFACE rsync://backup.server/directory

    Duplicity 0.6 series is being deprecated:
    See http://www.nongnu.org/duplicity/

    Synchronising remote metadata to local cache...
    Last full backup date: Mon Aug 28 20:40:03 2017
    Collection Status
    -----------------
    Connecting with backend: RsyncBackend
    Archive directory: /root/.cache/duplicity/71c92698cf8a96443a32a743fe691e89
    
    Found 1 secondary backup chain.
    Secondary chain 1 of 1:
    -------------------------
    Chain start time: Tue Aug 22 20:40:02 2017
    Chain end time: Sun Aug 27 20:40:03 2017
    Number of contained backup sets: 6
    Total number of contained volumes: 159
     Type of backup set:                            Time:   Number of volumes:
		    Full         Tue Aug 22 20:40:02 2017               154
	     Incremental         Wed Aug 23 20:40:03 2017                 1
	     Incremental         Thu Aug 24 20:40:03 2017                 1
	     Incremental         Fri Aug 25 20:40:04 2017                 1
	     Incremental         Sat Aug 26 20:40:03 2017                 1
	     Incremental         Sun Aug 27 20:40:03 2017                 1
    -------------------------


    Found primary backup chain with matching signature chain:
    -------------------------
    Chain start time: Mon Aug 28 20:40:03 2017
    Chain end time: Wed Aug 30 20:40:03 2017
    Number of contained backup sets: 3
    Total number of contained volumes: 128
     Type of backup set:                            Time:   Number of volumes:
		    Full         Mon Aug 28 20:40:03 2017               126
	     Incremental         Tue Aug 29 20:40:04 2017                 1
	     Incremental         Wed Aug 30 20:40:03 2017                 1
    -------------------------
    No orphaned or incomplete backup sets found.


# DESCRIPTION

`duplicity-ninja` inspects the backupninja configuration in
`/etc/backupninja.conf` and infers many of the options for duplicty
required to run duplicty, greatly simplifying the management of it.


# SEE ALSO

- backupninja: <https://labs.riseup.net/code/projects/backupninja/wiki>
- duplicity: <http://duplicity.nongnu.org/>

# AUTHOR

Nick Stokoe <github.wu-lee at noodlefactory.co.uk>

