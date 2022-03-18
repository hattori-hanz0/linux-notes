# SSH

Konfiguracja po stronie klienta `~/.ssh/config`

```
Host *
    IdentitiesOnly=yes

Host wrap
    Hostname 192.168.1.10
    User nazwa-użytkownika
    PasswordAuthentication no
    PubkeyAuthentication yes
    IdentityFile ~/.ssh/klucze/id_ecdsa_sk

Host 192.168.100.\*
	Port 22
	User admin
	KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1

Host 192.168.1.110
	Port 22
	User manager
	KexAlgorithms diffie-hellman-group1-sha1,curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1

Host tasksrv
	HostName asdf.lan
	User task-user
	Port 12722
	IdentityFile ~/.ssh/id_rsa
	LocalForward 53589 localhost:53589
	ServerAliveInterval 30
	ServerAliveCountMax 3

Host 192.168.2.222
    User qwerty
    HostKeyAlgorithms=+ssh-dss
```
