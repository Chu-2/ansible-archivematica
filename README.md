# Archivematica playbook

The provided playbook installs Archivematica on a server running Ubuntu Server 16.04.

## Requirements

- Ansible 2.2 or newer
- Python 2.7 installed on Ubuntu Server

## How to use

1. Download the Ansible roles.

  ```bash
  ansible-galaxy install -f -p roles/ -r requirements.yml
  ```

2. Create a user that can run `sudo` commands without password.

3. Add your public key to your newly created user on the server.

```bash
ssh-copy-id username@hostname
```

4. Modify the `hosts` file to use the appropriate hostname, ip address and username.

```bash
$ cat hosts
hostname ansible_host=xxx.xxx.xxx.xxx ansible_user=username
```

5. Modify the `singlenode.yml`'s hosts value to match the hostname in `hosts`.

6. Install and deploy Archivematica and its dependencies.

```bash
ansible-playbook singlenode.yml
```

The above command will take several minutes. If successful, the final output should indicate `unreachable=0 failed=0`.

Note: the `ansible-playbook singlenode.yml` command may fail initially. If it does, try it again.

7. Confirm that Archivematica and its dependencies are installed and working by navigating to your server's IP address (http://xxx.xxx.xxx.xxx).
  The Archivematica Storage Service should be being served at the same IP on port 8000, i.e., http://xxx.xxx.xxx.xxx:8000.

The default username and password for accessing the Storage Service are "test"
and "test". Once you log in, go to the "Administration" tab, then click "Users"
on the lefthand column, then click the "Edit" button of the "test" user, then
copy the API key at the bottom of the page to your clipboard.

Then navigate to the Archivematica dashboard (http://xxx.xxx.xxx.xxx), fill in
the form, and click "Create". When communication with the FPR Server has
completed, click the "continue" button. Now enter the API key that you copied
from the Storage Service and click the first button, the one labelled "Register
with the storage service & use default configuration."

You can test that your Archivematica installation works by performing a sample
Transfer and Ingest.
