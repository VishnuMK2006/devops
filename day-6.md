# Ansible Setup and Execution Guide (Ubuntu + AWS EC2)

## 1. Ansible Installation on Ubuntu

First, update your package list:

```bash
sudo apt update
```

Install Ansible:

```bash
sudo apt install ansible -y
```

Verify installation:

```bash
ansible --version
```
 <img width="809" height="578" alt="Screenshot from 2026-02-14 10-27-50" src="https://github.com/user-attachments/assets/2dc0ecc8-0e58-4980-895b-e67db9ed1e63" />


## 2. Repository Used for this Hands on.

Clone the Ansible project repository:

```bash
git clone https://github.com/jagadeeshkanna97/ansible-k.git
cd ansible-k
```

**Note master is your Local ubuntu and slave is your EC2 instances.*


## 3. Setup Slaves (AWS EC2 Ubuntu Instances)

### *Create One EC2 instance in AWS and note its required details below*
Instance name<br>
public IP<br>
instance name<br>
key_pair_value.pmk<br>

### Before run the terraform script

<img width="1869" height="853" alt="Screenshot from 2026-02-14 11-25-33" src="https://github.com/user-attachments/assets/bf3a6df6-e1c0-4ffa-a5a3-0a973ce25c14" />

## 4. Configure Inventory File

Edit the inventory file:

```bash
nano inventory.ini
```

Example configuration:

```ini
[slaves]
node1 ansible_host=<your_public_instance_id> ansible_user=<instance name> ansible_ssh_private_key_file=/path/to/key.pem
```

Explanation of parameters:

| Field                          | Meaning                            |
| ------------------------------ | ---------------------------------- |
| `[slaves]`                     | Group name                         |
| `node1`                        | Logical name of instance           |
| `ansible_host`                 | Public IP of EC2                   |
| `ansible_user`                 | Default SSH user (Ubuntu = ubuntu) |
| `ansible_ssh_private_key_file` | Path to .pem key                   |

  <img width="1607" height="1043" alt="Screenshot from 2026-02-14 11-26-14" src="https://github.com/user-attachments/assets/3e93dae3-980a-47b0-bd19-ced3267432c7" />

## 5. Test Connection to Slaves

### Command:

```bash
ansible -i inventory.ini slaves -m ping
```

Explanation:

| Part               | Purpose                  |
| ------------------ | ------------------------ |
| `-i inventory.ini` | Specifies inventory file |
| `slaves`           | Target group             |
| `-m ping`          | Uses Ansible ping module |



### Output:

```json
ansible | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

Meaning:

* SSH connection successful
* Python detected on remote machine
* Host reachable




## 6. Verbose Ping Test
### Command:

```bash
ansible -i inventory.ini slaves -m ping -vv
```

Explanation:

| Flag  | Purpose                        |
| ----- | ------------------------------ |
| `-vv` | Verbose output (debug details) |

Displays:

* Ansible version
* Python interpreter
* Module paths
* Execution steps

Useful for troubleshooting.



## 7. Execute Playbook

### Command:

```bash
ansible-playbook -i inventory.ini apache-playbook.yml
```

Explanation:

| Part                  | Purpose         |
| --------------------- | --------------- |
| `ansible-playbook`    | Runs a playbook |
| `-i inventory.ini`    | Inventory file  |
| `apache-playbook.yml` | Playbook name   |

What happens:

* Connects to slaves
* Executes defined tasks
* Example tasks:

  * Install Apache
  * Start service
  * Enable on boot


  <img width="1920" height="1200" alt="Screenshot from 2026-02-14 11-38-36" src="https://github.com/user-attachments/assets/5dc4aff2-efc2-4d41-bff9-550959bf21d2" />

## After script executed


  <img width="1847" height="986" alt="Screenshot from 2026-02-14 11-37-08" src="https://github.com/user-attachments/assets/87a723a8-668d-4e4c-9760-145fc81699e9" />

## Final output
  <img width="1847" height="986" alt="Screenshot from 2026-02-14 11-37-23" src="https://github.com/user-attachments/assets/835ceb75-8069-433e-956b-ba729b52e72d" />

# Ansible Explained

Ansible is an automation tool used to configure servers and manage infrastructure.

Instead of manually logging into each server:

* Writing commands repeatedly
* Installing software one by one
* Updating configurations manually

You define tasks once in a **playbook**, and Ansible:

* Connects to all servers
* Runs the tasks automatically
* Ensures consistency
* Ideal for DevOps, cloud, CI/CD

In simple terms:

Ansible lets you control many machines from one machine using automation.
