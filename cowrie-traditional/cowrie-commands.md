# Cowrie Traditional Honeypot Commands

This file documents Cowrie-related commands that were found in the Cowrie VM command history. These commands relate to configuring, running, updating, testing, and checking the traditional Cowrie SSH honeypot.

The purpose of this file is to document verified commands used during the project. It does not claim to be a full fresh installation guide from scratch.

## 1. Accessing the Cowrie User

The following command was used to switch into the dedicated Cowrie user account:

```bash
sudo -iu cowrie
```

## 2. Starting Cowrie

The following commands were used to start Cowrie from the dedicated Cowrie user account:

```bash
sudo -iu cowrie
cd /home/cowrie/cowrie
./cowrie-env/bin/cowrie start
```

If Cowrie is already running, the command returns:

```bash
cowrie is already running
```

## 3. Checking Cowrie Status

The following commands were used to check whether Cowrie was running:

```bash
systemctl status cowrie --no-pager
```

```bash
./cowrie-env/bin/cowrie status
```

## 4. Restarting Cowrie

The following command was used to restart the Cowrie service after changes:

```bash
sudo systemctl restart cowrie
```

## 5. Testing SSH Access to Cowrie

The following command was used to test SSH access to the Cowrie honeypot on port `2222`:

```bash
ssh user1@10.10.70.10 -p 2222
```

## 6. Checking GitHub Connectivity

The following commands were used to confirm that the Cowrie VM could reach GitHub:

```bash
ping -c 4 github.com
```

```bash
curl -I https://github.com
```

## 7. Updating Cowrie from GitHub

The following commands were used when checking and updating the local Cowrie repository:

```bash
git fetch --all
```

```bash
git log --oneline HEAD..origin/main
```

```bash
git pull --ff-only
```

## 8. Backing Up Cowrie Before Updating

The following command was used to create a backup of the Cowrie directory before updating:

```bash
cp -a cowrie cowrie_backup_before_update_$(date +%F_%H%M%S)
```

The following command was used to back up the modified Cowrie authentication file before updating:

```bash
cp -a /home/cowrie/cowrie/src/cowrie/core/auth.py /home/cowrie/auth.py.pre_update
```

## 9. Saving Local Changes Before Updating

The following Git commands were used to check and save local changes before applying updates:

```bash
git status --short
```

```bash
git stash push -u -m 'pre-update stash'
```

```bash
git stash list
```

```bash
git stash show --stat stash@{0}
```

```bash
git stash show --stat --include-untracked stash@{0}
```

```bash
git diff stash@{0}^1 stash@{0} -- src/cowrie/core/auth.py
```

## 10. Restoring Custom Cowrie Files

The following commands were used to restore selected customised Cowrie files after updating:

```bash
git checkout stash@{0} -- honeyfs
```

```bash
git checkout stash@{0} -- var/lib/cowrie/cmdoutput.json
```

```bash
git checkout stash@{0} -- var/lib/cowrie/fs.pickle
```

```bash
git checkout stash@{0} -- honeyfs/home
```

## 11. Editing Cowrie Authentication Behaviour

The following command was used to edit Cowrie's authentication file:

```bash
nano /home/cowrie/cowrie/src/cowrie/core/auth.py
```

This file was edited as part of customising the honeypot authentication behaviour.

## 12. Editing Cowrie Configuration

The following command was used to edit the Cowrie configuration file:

```bash
nano /home/cowrie/cowrie/etc/cowrie.cfg
```

## 13. Checking Cowrie Port and Authentication Settings

The following command was used to check whether Cowrie was listening on port `2222`:

```bash
ss -tlnp | grep 2222
```

The following command was also used with sudo privileges to check listening services on port `2222`:

```bash
sudo ss -tlnp | grep 2222
```

The following command was used to check the Cowrie authentication class setting in the configuration file:

```bash
grep -n "auth_class" /home/cowrie/cowrie/etc/cowrie.cfg
```

The following command was used to check the custom authentication class inside Cowrie's authentication file:

```bash
grep -R -n "class AuthAlwaysSucceed" /home/cowrie/cowrie/src/cowrie/core/auth.py
```

## 14. Customising the Cowrie Fake Filesystem

The following commands were used to inspect Cowrie's fake filesystem structure:

```bash
sudo -u cowrie -H bash -lc "ls -l /home/cowrie/cowrie/honeyfs"
```

```bash
sudo -u cowrie -H bash -lc "ls -l /home/cowrie/cowrie/honeyfs/home"
```

```bash
sudo -u cowrie -H bash -lc "ls -la /home/cowrie/cowrie/honeyfs/home/user1"
```

The following commands were used to create fake files for the `user1` account inside Cowrie's fake filesystem:

```bash
cd /home/cowrie/cowrie/honeyfs/home/user1
```

```bash
touch notes.txt passwords.txt .bash_history
```

```bash
echo "TODO: Update web server config" > notes.txt
```

```bash
echo "db_password=SuperSecret123" > passwords.txt
```

The following commands were used to create a fake `Documents` folder and a decoy notes file for `user1`:

```bash
mkdir -p honeyfs/home/user1/Documents
```

```bash
printf "TODO:\n- Review nginx logs\n- Check backups\n- Rotate admin password\n" > honeyfs/home/user1/Documents/notes.txt
```

## 15. Checking Cowrie Log Files

The following commands were used to inspect Cowrie log locations:

```bash
ls -lh /var/log/cowrie
```

```bash
ls -lh var/log/cowrie
```

```bash
tail -n 50 /home/cowrie/cowrie/var/log/cowrie/cowrie.json
```

```bash
sudo tail -n 50 /home/cowrie/cowrie/var/log/cowrie/cowrie.json.2026-04-15
```

```bash
sudo tail -n 50 /home/cowrie/cowrie/var/log/cowrie/cowrie.json.2026-04-25
```

## 16. Locating Cowrie Files

The following commands were used to locate Cowrie-related files and directories:

```bash
find /home -type d -name "cowrie" 2>/dev/null
```

```bash
sudo find / -type f -name "cowrie.json*" 2>/dev/null
```
