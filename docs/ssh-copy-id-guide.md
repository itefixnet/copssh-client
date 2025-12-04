# ssh-copy-id tool on Windows

[Copssh client](https://itefix.net/copssh/client) versions 8 and higher support the ssh-copy-id tool.

## Creating a Test Key Pair

```bash
bin\ssh-keygen -t ed25519 -f test
```

Output:
```
Generating public/private ed25519 key pair.
Enter passphrase for "test" (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in test
Your public key has been saved in test.pub
```

## Getting Help

```bash
bin\bash --login -c "ssh-copy-id -?"
```

Output:
```
Usage: /bin/ssh-copy-id [-h|-?|-f|-n|-s] [-i [identity_file]] [-p port] [-F alternative ssh_config file] [[-o <ssh -o options>] ...] [user@]hostname

-f: force mode -- copy keys without trying to check if they are already installed
-n: dry run    -- no keys are actually copied
-s: use sftp   -- use sftp instead of executing remote-commands. Can be useful if the remote only allows sftp
-h|-?: print this help
```

## Transferring the Public Key (Dry Run)

Test the key transfer without actually copying:

```bash
bin\bash --login -c "ssh-copy-id -n -i ./test a@localhost"
```

Output:
```
/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "./test.pub"
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
=-=-=-=-=-=-=-=
Would have added the following key(s):

ssh-ed25519 AAAA.....GG80e user@host
=-=-=-=-=-=-=-=
```

## Transferring the Public Key

Actually transfer the key to the remote server:

```bash
bin\bash --login -c "ssh-copy-id -i ./test a@localhost"
```

Output:
```
/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "./test.pub"
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
a@localhost's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'a@localhost'"
and check to make sure that only the key(s) you wanted were added.
```

## Transferring the Same Key Again

If you try to transfer a key that's already installed:

```bash
bin\bash --login -c "ssh-copy-id -i ./test a@localhost"
```

Output:
```
/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "./test.pub"
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/bin/ssh-copy-id: WARNING: All keys were skipped because they already exist on the remote system.
                (if you think this is a mistake, you may want to use -f option)
```

## See Also

- [ssh-copy-id man page](ssh-copy-id-man-page.md)
- [Copssh client homepage](https://itefix.net/copssh/client)
