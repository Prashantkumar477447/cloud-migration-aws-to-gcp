### ☁️ Cloud Migration Project — AWS EC2 → GCP Compute Engine

---

### 🧩 **Overview**

This project demonstrates a **simple, end-to-end cloud migration** workflow by hosting a static HTML website on **AWS EC2** and migrating it to **Google Cloud Compute Engine**.

It showcases the fundamentals of multi-cloud deployment, web hosting, and file migration between two major cloud providers.

---

### ⚙️ **Tech Stack**

* **Cloud Platforms:** AWS, GCP
* **Compute Services:** EC2 (AWS), Compute Engine (GCP)
* **Web Server:** Apache2
* **Operating System:** Ubuntu 22.04 LTS
* **Tools:** SSH, SCP, zip/unzip, Browser-based SSH

---

## 🚀 **Project Flow**

---

### 🧱 **Phase 1: Host Website on AWS EC2**

#### Step 1. Create EC2 Instance

* AMI: Ubuntu 22.04 LTS
* Type: `t2.micro`
* Key Pair: `html-demo-server-key.pem`
* Security Group: ✅ Allow HTTP, ✅ Allow SSH

📸 **Screenshot:**
![AWS EC2 Instance](images/aws-ec2-instance.png)

---

#### Step 2. Connect to EC2

```bash
# Use EC2 Instance Connect (browser-based SSH)
```

---

#### Step 3. Install Apache

```bash
sudo apt update
sudo apt install -y apache2
sudo systemctl enable --now apache2
```

---

#### Step 4. Create HTML Page

```bash
cd /var/www/html
sudo rm index.html
echo "<h1>Hello from AWS EC2!</h1>" | sudo tee /var/www/html/index.html
```

---

#### Step 5. Test in Browser

Visit:

```
http://<EC2-Public-IP>/
```

📸 **Screenshot:**
![AWS Website Output](images/aws-website.png)

✅ Output: “Hello from AWS EC2!”

---

### 📦 **Phase 2: Backup Website from AWS**

#### Step 6. Zip & Download Website Files

```bash
cd /var/www/html
sudo apt install -y zip
sudo zip -r /tmp/website.zip /var/www/html
```

Download via browser SSH → ⚙️ → **File transfer → Download `/tmp/website.zip`**

📸 **Screenshot:**
![AWS Backup File](images/aws-backup.png)

✅ Backup complete!

---

### 🌩 **Phase 3: Migrate to GCP Compute Engine**

#### Step 7. Create GCP VM

* Name: `gcp-html-server`
* OS: Ubuntu 22.04 LTS
* Type: `e2-micro`
* Firewall: ✅ Allow HTTP traffic

📸 **Screenshot:**
![GCP VM Creation](images/gcp-vm-creation.png)

---

#### Step 8. Connect via SSH (Browser)

Click “SSH → Open in browser window”.

---

#### Step 9. Install Apache

```bash
sudo apt update
sudo apt install -y apache2 unzip
sudo systemctl enable --now apache2
```

---

#### Step 10. Upload and Extract Website

1. In **GCP Console → Compute Engine → VM instances → ⋮ → Upload file**
2. Choose your `website.zip` file.
3. Move and unzip:

   ```bash
   sudo mv website.zip /var/www/html/
   cd /var/www/html
   sudo unzip website.zip
   sudo mv var/www/html/* /var/www/html/
   sudo rm -rf var
   sudo chown -R www-data:www-data /var/www/html
   sudo chmod -R 755 /var/www/html
   sudo systemctl restart apache2
   ```

📸 **Screenshot:**
![GCP Upload File](images/gcp-upload.png)

---

### 🌍 **Step 11. Test in Browser**

Visit:

```
http://<GCP-External-IP>/
```

📸 **Screenshot:**
![GCP Website Output](images/gcp-website.png)

✅ You’ll see your same HTML page — successfully migrated from AWS to GCP!

---

## 📊 **Final Verification**

| Cloud | Service        | Status | Result                        |
| ----- | -------------- | ------ | ----------------------------- |
| AWS   | EC2            | ✅      | Website hosted                |
| GCP   | Compute Engine | ✅      | Website migrated successfully |

 create a **folder structure (with README + `/images/` subfolder + .gitignore + license template)** as a ready-to-push GitHub project zip?
