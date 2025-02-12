## Enum4Linux Summary EXPLANATION (use -a)

- **Purpose**: Enumerates SMB shares on Windows/Linux systems.
- **Function**: Wrapper for Samba tools to extract SMB information easily.
- **Availability**: Pre-installed on AttackBox; installable from GitHub.

###### Syntax:

```bash
enum4linux [options] ip
```

###### Common Tags and Functions:

- **-U**: Get user list
- **-M**: Get machine list
- **-N**: Get namelist dump (different from -U and -M)
- **-S**: Get share list
- **-P**: Get password policy info
- **-G**: Get group and member list
- **-a**: Full enumeration (all options above)


here i used 
enum4linux 10.10.212.180 -a


![[Pasted image 20250107192757.png]]



## linpeas 

use it after braking into a machine use scp to upload it to the machine if you have creds 

### SCP STUFF

/dev/shm : shared files

```sh
scp <file> username@ip:/dev/shm 
```