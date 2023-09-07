# Security

This folder contains ressources about security related topics.

## Operating systems

### Ubuntu

- [Default file permissions](https://www.vidarholen.net/contents/junk/ubuntu_permissions.html)
    - `sudo find / /boot -xdev ! -type s -printf 'chmod %m %p\n' -printf 'chown %u:%g %p\n' `
