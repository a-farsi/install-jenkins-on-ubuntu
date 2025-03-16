# install-jenkins-on-ubuntu

To install Jenkins on Ubuntu 22.04 from scratch, we need to run the following commands:  


#### Summary of Commands
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y openjdk-17-jre
sudo apt update && sudo apt upgrade -y
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl enable --now jenkins
sudo ufw allow 8080/tcp
sudo ufw reload
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Here is the step by step explanation:

#### Step 1: Update the System
Ensure that our system is up to date before installation:

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install Java
Jenkins requires Java 11 or later. We Install OpenJDK 17 :

```bash
sudo apt install -y openjdk-17-jre
```
We verify the installation:

```bash
java -version
```

### Step 3: Add Jenkins Repository
Jenkins is not included in the default Ubuntu repositories, so add the official Jenkins repository:

Add the Jenkins GPG key:

```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```
Add the Jenkins repository:

```bash
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```
Update package lists:

```bash
sudo apt update
```
### Step 4: Install Jenkins
Now, we install Jenkins:

```bash
sudo apt install -y jenkins
```

### Step 5: Start and Enable Jenkins Service
We start the Jenkins service:

```bash
sudo systemctl start jenkins
```
Enable Jenkins to start at boot:

```bash
sudo systemctl enable --now jenkins
```
Check if Jenkins is running:

```bash
sudo systemctl status jenkins
```

### Step 6: Open Firewall Ports (If UFW is Enabled)
Jenkins runs on port 8080 by default. If UFW (Uncomplicated Firewall) is enabled, we can allow Jenkins as follows:

```bash
sudo ufw allow 8080/tcp
sudo ufw reload
```
To check UFW status:

```bash
sudo ufw status
```
Step 7: Access Jenkins Web UI
Open your browser and go to:

```cpp
http://<our-server-ip>:8080
```
If running locally, use:

```cpp
http://localhost:8080
```
Retrieve the initial admin password: Run the following command to get the initial password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Then, we follow the Jenkins setup wizard, install suggested plugins, and create an admin user.

### Step 8: (Optional) Change Jenkins Port
If we want to run Jenkins on a different port (e.g., 9090):

we open the Jenkins configuration file:

```bash
sudo nano /etc/default/jenkins
```
and we modify the line:

```bash
HTTP_PORT=9090
```
Finally, we restart Jenkins:

```bash
sudo systemctl restart jenkins
```

Now, we can access Jenkins at:

```cpp
http://<your-server-ip>:9090
```
