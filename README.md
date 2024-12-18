# Snowflake
Summary notes on snowflake.

## SnowSQL Installation

### 0. Linux Container

The `--platform linux/x86_64` is needed on M1 macbook [credit](https://stackoverflow.com/a/69075554).

```
docker run --platform linux/x86_64 -d -t -p 8080:80 --name ux86 ubuntu:22.04
```

Check running containers via `docker ps`:
```
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS          PORTS                  NAMES
976ee267c662   ubuntu:22.04   "/bin/bash"   58 seconds ago   Up 57 seconds   0.0.0.0:8080->80/tcp   ux86
```

bash on the container:
```
docker exec -it ux86 bash
```

Install packages:
```
apt install curl gpg zip unzip
```


### 1: Download

```shell
# download the installer (AWS)
curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash

# download the key
curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash.sig

# dowanload the public key from the keyserver
# SnowSQL 1.2.24 and higher
gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 630D9F3CAB551AF3
```

<details>

```
root@976ee267c662:~/temp# curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 47.9M  100 47.9M    0     0  7259k      0  0:00:06  0:00:06 --:--:-- 7641k
root@976ee267c662:~/temp# curl -O https://sfc-repo.snowflakecomputing.com/snowsql/bootstrap/1.3/linux_x86_64/snowsql-1.3.2-linux_x86_64.bash.sig
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   543  100   543    0     0    926      0 --:--:-- --:--:-- --:--:--   937
root@976ee267c662:~/temp# gpg --keyserver hkp://keyserver.ubuntu.com --recv-keys 630D9F3CAB551AF3
gpg: directory '/root/.gnupg' created
gpg: keybox '/root/.gnupg/pubring.kbx' created
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key 630D9F3CAB551AF3: public key "Snowflake Computing (Snowflake Computing Gpg Key) <snowflake_gpg@snowflake.net>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```
  
</details>


### 2. Verify
```
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

### 3: Install

```shell
# install SnowSQL
bash snowsql-1.3.2-linux_x86_64.bash

# Check version
~/bin/snowsql -v
# Version: 1.3.2
```

<details>
  
```
root@976ee267c662:~/temp# bash snowsql-1.3.2-linux_x86_64.bash
**********************************************************************
 Installing SnowSQL, Snowflake CLI.
**********************************************************************

Specify the directory in which the SnowSQL components will be installed. [~/bin] 
Do you want to add /root/bin to PATH in /root/.profile? [y/N] y
Updating /root/.profile to have /root/bin in PATH
Open a new terminal session to make the updated PATH take effect.
**********************************************************************
 Congratulations! Follow the steps to connect to Snowflake DB.
**********************************************************************

1. Open a new terminal window.
2. Execute the following command to test your connection:
      snowsql -a <account_name> -u <login_name>

      Enter your password when prompted. Enter !quit to quit the connection.

3. Add your connection information to the ~/.snowsql/config file:
      accountname = <account_name>
                username = <login_name>
                password = <password>

4. Execute the following command to connect to Snowflake:

      snowsql

See the Snowflake documentation <https://docs.snowflake.net/manuals/user-guide/snowsql.html> for more information.

root@976ee267c662:~# ~/bin/snowsql -v
Version: 1.3.2
```

</details>








