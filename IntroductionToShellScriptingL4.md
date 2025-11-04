##  Shell Scripting – Important Terms & Concepts

* **Shebang (`#!`)** → First line of a script, tells which shell to use → Example: `#!/bin/bash`
* **/bin/bash vs /bin/sh**

  * `/bin/bash` → Feature-rich (arrays, functions, string ops, `[[ ]]`)
  * `/bin/sh` → Basic, portable, fewer features
* **echo** → Prints text → `echo "Hello"`
* **Variables** → `name="John"` | Use: `${name}`
* **Parameter Expansion** → `${var}` | `${var^^}` (uppercase) | `${var,,}` (lowercase)
* **Command Substitution** → `$(command)` → Example: `echo "Time: $(date)"`
* **Arithmetic Expansion** → `$((a + b))` → Example: `sum=$((x + y))`
* **read command** → Takes input → `read -p "Enter name: " name`
* **if condition**

  ```bash
  if [ condition ]; then
    commands
  fi
  ```
* **Bash-specific conditions** → `[[ condition ]]`
* **Loops**

  ```bash
  for i in {1..5}; do
    echo $i
  done
  ```
* **Functions**

  ```bash
  func_name() {
    commands
  }
  ```
* **source / dot command** → Import another script → `source utils.sh`
* **File permissions** → r (read), w (write), x (execute) → for user, group, others
* **chmod** → Make executable → `chmod +x script.sh`

## 🔹 Common Useful Commands

| Purpose               | Command                          |
| --------------------- | -------------------------------- |
| Current date/time     | `date`                           |
| Disk usage            | `df -h`                          |
| List files            | `ls -l`                          |
| Check user exists     | `id username`                    |
| Internet connectivity | `ping -c 1 8.8.8.8`              |
| System uptime         | `uptime -p`                      |
| Backup directory      | `tar -czf backup.tar.gz folder/` |

## 🔹 ACL (Access Control List)

* **What is ACL?** → Fine-grained file permissions for specific users/groups
* **Check ACL enabled** → `mount | grep acl`
* **View ACLs** → `getfacl filename`
* **Set ACL (user permission)** → `setfacl -m u:john:r-- file.txt`
* **Set ACL for group** → `setfacl -m g:devs:rw- file.txt`
* **Remove ACL entry** → `setfacl -x u:john file.txt`
* **Remove all ACLs** → `setfacl -b file.txt`
* **Recursive ACL on directory** → `setfacl -R -m u:john:rwX /var/www`
* **Default ACL for new files** → `setfacl -d -m u:john:rwX /var/www`
