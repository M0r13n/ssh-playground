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

## Revocation

Add this line to `/etc/ssh/sshd_config`:

`RevokedKeys /etc/ssh/revoked_keys`

Create the `/etc/ssh/revoked_keys` file with appropiate permissions.

Add the public key (not the certificate) to the file (plain text)

Output:

```txt
error: Authentication key RSA SHA256:WTpdo6u+9ghr7/s9bqBDJt1DHTnUQdyn4Vl5a0thMkg revoked by file /etc/ssh/revoked_keys
error: Authentication key RSA-CERT SHA256:WTpdo6u+9ghr7/s9bqBDJt1DHTnUQdyn4Vl5a0thMkg revoked by file /etc/ssh/revoked_keys
```
