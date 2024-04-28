# evil-winrm-fix
Fix the Error: An error of type OpenSSL::Digest::DigestError happened, message is Digest initialization failed: initialization error evil-winrm error.

## Fix
Fix this error is pretty simple and only require some change on the /etc/ssl/openssl.cnf file.

1) edit /etc/ssl/openssl.cnf by adding legacy = legacy_sect under default = default_sect in order to appear as:
```
[openssl_init]
providers = provider_sect

# List of providers to load
[provider_sect]
default = default_sect
legacy = legacy_sect
```
2) uncommenting #activate = 1 under [default_sect] and adding [legacy_sect] and activate = 1 under them in order to appear as:
```
[default_sect]
activate = 1
[legacy_sect]
activate = 1
```

I've discovered this workaround after some problem during a CTF, so i decided to release a fix for anyone.
