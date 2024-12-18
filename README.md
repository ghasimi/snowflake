# Snowflake
Summary notes on snowflake.

## SnowSQL Installation

### 1: Download and Verify

```shell
# download the installer (AWS)
curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash

# download the key
curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash.sig

# install GPG if not availble
apt install gpg

# dowanload the public key from the keyserver
# SnowSQL 1.2.24 and higher
gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 630D9F3CAB551AF3

# verify
gpg --verify snowsql-1.3.2-linux_x86_64.bash.sig snowsql-1.3.2-linux_x86_64.bash
```

Output:
```
gpg: Signature made Thu Aug  8 10:49:39 2024 UTC
gpg:                using RSA key 630D9F3CAB551AF3
gpg: Good signature from "Snowflake Computing (Snowflake Computing Gpg Key) <snowflake_gpg@snowflake.net>" [expired]
gpg: Note: This key has expired!
Primary key fingerprint: 23D8 08A5 B09A 9CB3 4610  C0B2 630D 9F3C AB55 1AF3
```

Delete the public key for security.
```
gpg --delete-key "Snowflake Computing"
```

Output:
```
gpg (GnuPG) 2.2.27; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.


pub  rsa4096/630D9F3CAB551AF3 2022-09-20 Snowflake Computing (Snowflake Computing Gpg Key) <snowflake_gpg@snowflake.net>

Delete this key from the keyring? (y/N) y
```

