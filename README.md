# Linux Commands

### `history`
- **Description**: Displays the history of commands entered in the terminal.
- **Usage**: 
  ```sh
  history
  ```

### `groupadd "GROUP_NAME"`
- **Description**: Creates a new group with the specified name.
- **Usage**: 
  ```sh
  groupadd "GROUP_NAME"
  ```

### `useradd -g "ASSIGNED_GROUP" "USER_NAME"`
- **Description**: Creates a new user and assigns them to the specified group. Note that a user cannot be created without being assigned to a group.
- **Usage**: 
  ```sh
  useradd "USER_NAME" "ASSIGNED_GROUP"
  ```

### `rm -r "DIR_NAME"`
- **Description**: Removes a directory and all its contents.
- **Usage**: 
  ```sh
  rm -r "DIR_NAME"
  ```

### `rm -d "DIR_NAME"`
- **Description**: Removes an empty directory.
- **Usage**: 
  ```sh
  rm -d "DIR_NAME"
  ```

### `cat /etc/group`
- **Description**: Lists all groups on the system.
- **Usage**: 
  ```sh
  cat /etc/group
  ```

### `su - "USER_NAME"`
- **Description**: Changes the current user to the specified user.
- **Usage**: 
  ```sh
  su - "USER_NAME"
  ```

### `umask`
- **Description**: Sets the file creation mask, which determines the default permission bits for newly created files and directories. The umask value is subtracted from the default permission values (666 for files and 777 for directories) to determine the actual permissions.
- **Usage**:
  ```sh
  umask 022
  ```

### `ll`
- **Description**: An alias for `ls -al`, which lists all files and directories in the current directory in long format, including hidden files.
- **Usage**: 
  ```sh
  ll
  ```

### `ll /etc/`
- **Description**: Lists all files and directories in the `/etc/` directory in long format, including hidden files.
- **Usage**: 
  ```sh
  ll /etc/
  ```

### `~`
- **Description**: Represents the home directory of the current user.
- **Usage**: 
  ```sh
  cd ~
  ```

### `/opt/`
- **Description**: A directory for installing optional software.
- **Usage**: 
  ```sh
  cd /opt/
  ```

### `/tmp/`
- **Description**: A directory for temporary files. It is a safe space for work, and everything in it can be deleted.
- **Usage**: 
  ```sh
  cd /tmp/
  ```

### `df`
- **Description**: Displays disk space usage for all mounted file systems.
- **Usage**: 
  ```sh
  df
  ```

### `df -h`
- **Description**: Displays disk space usage in a human-readable format.
- **Usage**: 
  ```sh
  df -h
  ```

### `du`
- **Description**: Displays disk usage of files and directories.
- **Usage**: 
  ```sh
  du
  ```

### `du | sort -h`
- **Description**: Sorts the disk usage of files and directories in human-readable format (e.g., KB, MB, GB).
- **Usage**: 
  ```sh
  du | sort -h
  ```

### `echo "Ahoj" > test.txt`
- **Description**: Creates a file named `test.txt` and writes the text "Ahoj" to it.
- **Usage**: 
  ```sh
  echo "Ahoj" > test.txt
  ```

### `|`
- **Description**: A pipe, used to pass the output of one command as the input to another command. This allows commands to be executed simultaneously.
- **Usage**: 
  ```sh
  command1 | command2
  ```

# iptables Rules Explanation

## Enable Port 80

```sh
iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT\
```

This command allows incoming TCP traffic on port 80 (HTTP). Here's a breakdown of the options used:
- `-A INPUT`: Appends this rule to the INPUT chain.
- `-p tcp`: Specifies the protocol to match (TCP).
- `-m tcp`: Loads the TCP module.
- `--dport 80`: Specifies the destination port as 80.
- `-j ACCEPT`: Accepts (allows) the matched packets.

## Enable SSH from a Specific IP Address

```sh
iptables -A INPUT -p tcp -s 192.168.1.100 -m tcp --dport 22 -j ACCEPT
```

This command allows incoming TCP traffic on port 22 (SSH) from the IP address 192.168.1.100. Explanation:
- `-s 192.168.1.100`: Matches packets coming from IP address 192.168.1.100.
- `--dport 22`: Specifies the destination port as 22 (SSH).
- `-j ACCEPT`: Accepts (allows) the matched packets.

## Deny All Traffic from a Specific IP Address

```sh
iptables -A INPUT -s 192.168.1.200 -j DROP
```

This command drops (blocks) all incoming traffic from the IP address 192.168.1.200. Explanation:
- `-s 192.168.1.200`: Matches packets coming from IP address 192.168.1.200.
- `-j DROP`: Drops (blocks) the matched packets.

## Open a Range of Ports

```sh
iptables -A INPUT -m state --state NEW -m multiport --dports 1000:2000 -j ACCEPT
```

This command allows incoming TCP traffic on ports 1000 to 2000. Explanation:
- `-m state --state NEW`: Matches packets that are initiating a new connection.
- `-m multiport --dports 1000:2000`: Specifies the range of destination ports from 1000 to 2000.
- `-j ACCEPT`: Accepts (allows) the matched packets.

## Delete a Specific iptables Rule

To delete a specific iptables rule that allows SSH traffic from IP address 192.168.1.100 on port 22, use the following command:

```sh
iptables -D INPUT -p tcp -s 192.168.1.100 -m tcp --dport 22 -j ACCEPT
```

- **Explanation:**
  - `-D INPUT`: Deletes a rule from the INPUT chain.
  - `-p tcp`: Specifies the protocol of the rule to be deleted (TCP).
  - `-s 192.168.1.100`: Specifies the source IP address of the rule to be deleted.
  - `-m tcp`: Loads the TCP module to match TCP packets.
  - `--dport 22`: Specifies the destination port of the rule to be deleted (port 22).
  - `-j ACCEPT`: Specifies the target action of the rule to be deleted (ACCEPT).

---

## List iptables Rules with Line Numbers

To list all iptables rules along with their line numbers, use the following command:

```sh
iptables -L --line-numbers
```

- **Explanation:**
  - `-L`: Lists all rules in the specified chain (INPUT, OUTPUT, or FORWARD).
  - `--line-numbers`: Displays rules with line numbers, making it easier to reference specific rules.

---

## Delete a Specific iptables Rule by Line Number

To delete a specific iptables rule by its line number from the INPUT chain, use the following command:

```sh
iptables -D INPUT 3
```

- **Explanation:**
  - `-D INPUT`: Deletes a rule from the INPUT chain.
  - `3`: Specifies the line number of the rule to be deleted.

---

## Saving iptables Rules Permanently

To save iptables rules permanently to the file `/etc/sysconfig/iptables` (for CentOS/RHEL) or `/etc/iptables/rules.v4` (for Debian/Ubuntu), use the following command:

service iptables save

- **Explanation:**
  - `service iptables save`: Saves the current iptables rules to the appropriate configuration file for automatic loading at boot time.

### `chmod +x "FILE_NAME"`
- **Description**: Add the executable permission to the file variables_demo.sh for the user, group, and others (global).
- **Usage**: 
  ```sh
  chmod +x variables.sh
  ```

  ```bash

# Basic bash scripting
- **Description**: This is the content of a file named variables.sh
- **Usage**: Execute the script with this command:`./variables.sh "ARGUMENT`
  where "ARGUMENT" is boolean, number, string...
## Define a string variable
`VAR_STRING="string"`

## Define a numeric variable
`VAR_NUM=123456`

## Define a boolean variable
`VAR_BOOL=true`

## Assign the current username to a variable using command substitution
`VAR_PARAM="$(whoami)"`

## Create a new variable combining VAR_PARAM and the current date and time
`NEW_VAR_NAME=${VAR_PARAM}_with_the_$(date +%Y-%m-%d_%H%M%S)`

## Assign the first script argument to a variable
`VAR_NAME1=$1`

## Print the variables
`echo "VAR_STRING: $VAR_STRING"`

`echo "VAR_NUM: $VAR_NUM"`

`echo "VAR_BOOL: $VAR_BOOL"`

`echo "VAR_PARAM: $VAR_PARAM"`

`echo "NEW_VAR_NAME: $NEW_VAR_NAME"`

`echo "VAR_NAME1: $VAR_NAME1"`

## Demonstrate the difference in output with variable usage in strings
`myname=$(whoami)`

`echo "Using double quotes: My name is $myname."`

`echo 'Using single quotes: My name is $myname.'`

# Variable Comparisons and Printing Results

```bash
VAR_BOOL=true
VAR_PARAM="$(whoami)"

NEW_VAR_NAME=${VAR_PARAM}_with_the_$(date +%Y-%m-%d_%H%M%S)

VAR_NAME=$1
VAR_SURNAME=$2

# Print the variables
echo "VAR_STRING: $VAR_STRING"
echo "VAR_NUM: $VAR_NUM"
echo "VAR_BOOL: $VAR_BOOL"
echo "VAR_PARAM: $VAR_PARAM"
echo "NEW_VAR_NAME: $NEW_VAR_NAME"
echo "VAR_NAME: $VAR_NAME"

# Difference in output with variable usage in strings
myname=$(whoami)
echo "Using double quotes: My name is $myname."
echo 'Using single quotes: My name is $myname.'

# Variable comparisons and printing results
VAR_COND1="[ $VAR_NAME = $VAR_SURNAME ]"
VAR_COND2="[ $VAR_NAME != 'string' ]"
VAR_COND3="[ $VAR_NUM -eq 10 ]"
VAR_COND4="[ $VAR_NUM -ne 10 ]"

echo "Condition 1: [ $VAR_NAME = $VAR_SURNAME ]"
if [ "$VAR_NAME" = "$VAR_SURNAME" ]; then
    echo "Condition 1 is true."
else
    echo "Condition 1 is false."
fi

echo "Condition 2: [ $VAR_NAME != 'string' ]"
if [ "$VAR_NAME" != "string" ]; then
    echo "Condition 2 is true."
else
    echo "Condition 2 is false."
fi

echo "Condition 3: [ $VAR_NUM -eq 10 ]"
if [ "$VAR_NUM" -eq 10 ]; then
    echo "Condition 3 is true."
else
    echo "Condition 3 is false."
fi

echo "Condition 4: [ $VAR_NUM -ne 10 ]"
if [ "$VAR_NUM" -ne 10 ]; then
    echo "Condition 4 is true."
else
    echo "Condition 4 is false."
fi
```

# Description

## Variable Definitions (`VAR_NAME`, `VAR_SURNAME`, `VAR_NUM`):

- These variables store values used for comparisons (`$1` and `$2` are expected to be provided as command line arguments for `VAR_NAME` and `VAR_SURNAME` respectively).

## Condition 1 (`[ $VAR_NAME = $VAR_SURNAME ]`):

- Checks if `VAR_NAME` is equal to `VAR_SURNAME`.
- Prints whether Condition 1 is true or false based on the comparison result.

## Condition 2 (`[ $VAR_NAME != 'string' ]`):

- Checks if `VAR_NAME` is not equal to the string "string".
- Prints whether Condition 2 is true or false based on the comparison result.

## Condition 3 (`[ $VAR_NUM -eq 10 ]`):

- Checks if `VAR_NUM` is equal to 10.
- Prints whether Condition 3 is true or false based on the comparison result.

## Condition 4 (`[ $VAR_NUM -ne 10 ]`):

- Checks if `VAR_NUM` is not equal to 10.
- Prints whether Condition 4 is true or false based on the comparison result.

## Output Format:

- Each condition is echoed with its corresponding `[ ]` bracketed expression.
- Uses `if` statements to evaluate each condition and prints the result ("true" or "false").

## Usage:

- Save the script into a file named `variable_comparisons.sh`.
- Make sure the script is executable (`chmod +x variable_comparisons.sh`).
- Execute the script (`./variable_comparisons.md` or `bash variable_comparisons.sh`) to see the comparison results based on the current values of `VAR_NAME` and `VAR_NUM`.
