Collection of guides and ressources regarding GPG encryption

- [How to GPG and Yubikey, YouTube](https://www.youtube.com/watch?v=rGZtlgNhAVU&list=PLmoQ11MXEmahVl_uJVH0-a3XJtMV59PBu&ab_channel=402PaymentRequired)
- [YubiKey Guide](https://github.com/drduh/YubiKey-Guide)
- Generating secure passphrases
	- [Diceware](https://diceware.dmuth.org/)
	- [Wordlist](https://theworld.com/~reinhold/dicewarewordlist.pdf)

## GPG and SSH agent passthrough via SSH

On the SSH client add the following to `~/.ssh/config`

```config
Host remote_host
    RemoteForward _remote_agent_socket_ _local_agent_extra_socket_
    RemoteForward _remote_agent_ssh_socket_ _local_agent_ssh_socket_
```

For more details, see section 6.7: [GnuPG - ArchWiki](https://wiki.archlinux.org/title/GnuPG)
To forward the SSH agent to the remote host, also add the following:

```config
ForwardAgent yes
```

On the remote SSH server add the following inside `/etc/ssh/sshd_config`

```config
StreamLocalBindUnlink yes # For GPG
PermitTunnel yes # For SSH
```

See also my notes regarding [security](../setup/Security.md) on my homelab setup.

#gpg #passwords #security 