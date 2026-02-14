# AWS Documentation

## 1. Sign in to AWS Console

1. Open: [https://aws.amazon.com/console/](https://aws.amazon.com/console/)
2. Log in with your AWS account.


## 2. Navigate to EC2

1. In the AWS Console search bar, type **EC2**
2. Click **EC2** → Opens EC2 Dashboard


## 3. Launch Instance

1. Click **Launch Instance**


## 4. Choose an Amazon Machine Image (AMI)

Select a **Free Tier Eligible** AMI:

Recommended:

* **Ubuntu Server 22.04 LTS** (Free tier eligible)

Click **Select**

<img width="1920" height="1114" alt="Screenshot from 2026-02-13 11-31-05" src="https://github.com/user-attachments/assets/f2ab704b-c751-4010-aea7-b867988159df" />

## 5. Choose Instance Type

Select:

```
t3.micro
```

Reason:

* Free tier eligible

Click **Next**


## 6. Configure Instance Details

Usually keep defaults:

* Number of instances → 1
* Network → Default VPC
* Auto-assign Public IP → **Enable**

Click **Next**


## 7. Add Storage

Default is fine:

```
8 GB (Free Tier Eligible)
```

Click **Next**

<img width="1920" height="1114" alt="Screenshot from 2026-02-13 11-31-25" src="https://github.com/user-attachments/assets/4099e7d3-1c18-448c-ae40-4004dc3c16c2" />

## 8. Add Tags (Optional but Recommended)

Example:

| Key  | Value          |
| ---- | -------------- |
| Name | MyUbuntuServer |

<img width="1920" height="1114" alt="Screenshot from 2026-02-13 11-31-19" src="https://github.com/user-attachments/assets/13bbc76e-f2a8-42e9-855e-f53a7dde9b94" />

Click **Next**



## 9. Configure Security Group

Create a new security group:

Add rule:

| Type | Protocol | Port | Source              |
| ---- | -------- | ---- | ------------------- |
| SSH  | TCP      | 22   | My IP (Recommended) |

For testing (less secure):

```
Source → Anywhere (0.0.0.0/0)
```

Click **Review and Launch**


## 10. Select / Create Key Pair

Choose:

### Option A: Create New Key Pair

1. Select **Create new key pair**
2. Name → `my-key`
3. Format → **.pem**
4. Click **Download Key Pair**

Save file securely.


Click **Launch Instance**


## 11. Copy Public IP Address

Select instance → Copy:

```
Public IPv4 address
```

Example:

```
3.110.xxx.xxx
```

<img width="1920" height="1114" alt="Screenshot from 2026-02-13 11-30-22" src="https://github.com/user-attachments/assets/8e01eaf3-6e0a-454c-adaa-286c41046600" />

# Connect to EC2 from Ubuntu Terminal



## 12. Move Key Pair to Safe Location

Example:

```bash
mv ~/Downloads/my-key.pem ~/
```



## 13. Set Correct Permissions

```bash
chmod 400 ~/my-key.pem
```

Required for SSH security.

---

## 14. Connect via SSH

For Ubuntu AMI:

```bash
ssh -i ~/my-key.pem ubuntu@<public-ip>
```

Example:

```bash
ssh -i ~/my-key.pem ubuntu@3.110.xxx.xxx

```
