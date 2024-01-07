## Final

Copy the public key of the CA to the server:

```bash
scp ./ca/foo_ca.pub pi@pihole.local
```

Store it under `/etc/ssh`:

`sudo mv ./foo_ca.pub /etc/ssh/`

Fix permissions:

`sudo chown root:root /etc/ssh/foo_ca.pub`

Add this line to `/etc/ssh/sshd_config`:

`TrustedUserCAKeys /etc/ssh/foo_ca.pub`

Restart:

`systemctl restart sshd`

SSH using the key:

`ssh pi@pihole.local -i ./keys/user-key  -v`
# ssh-playground
