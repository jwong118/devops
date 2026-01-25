Here is the blog post converted into a clean, ready-to-use GitHub `README.md` format.

---

```markdown
# How to Install OpenShift Local (CRC) on RHEL 10

A step-by-step guide to spinning up a minimal OpenShift cluster on your local Red Hat Enterprise Linux 10 machine. 

This guide is adapted from [Donald Sebastian Leung's blog](https://donaldsebleung.com/blog/20240114-exploring-openshift-with-crc) and updated specifically for RHEL 10 workflows.

## 📋 Prerequisites

OpenShift is resource-intensive. Ensure your machine meets these minimum requirements before proceeding:

* **OS:** Red Hat Enterprise Linux 10 (Desktop environment recommended)
* **CPU:** 4 physical cores (8 vCPUs)
* **RAM:** 16 GB minimum (8 GB is insufficient)
* **Storage:** At least 35 GB of free space


---

## 🚀 Installation Guide

### Step 1: Prepare the RHEL 10 Environment
RHEL 10 requires specific virtualization tools to manage the cluster. Install `NetworkManager` for connectivity and `libvirt` for VM management.

```bash
sudo dnf install libvirt NetworkManager

```

### Step 2: Download OpenShift Local

Avoid using outdated `wget` links. Download the latest binary directly from Red Hat to ensure kernel compatibility.

1. Navigate to the [Red Hat Hybrid Cloud Console](https://www.google.com/search?q=https://console.redhat.com/openshift/create/local).
2. Log in with your Red Hat credentials.
3. Select **Linux** and click **Download OpenShift Local**.
4. **Important:** Download the **Pull Secret** (`pull-secret.txt`) from the same page. You will need this to authenticate your cluster.

### Step 3: Install the CRC Binary

Extract the downloaded archive and move the binary to a location in your system path.

```bash
# 1. Extract the archive
cd ~/Downloads
tar xvf crc-linux-amd64.tar.xz

# 2. Create a bin directory (if it doesn't exist) and move the binary
mkdir -p ~/bin
cp crc-linux-*-amd64/crc ~/bin/

# 3. Add to PATH (if strictly necessary)
echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc
source ~/.bashrc

```

Verify the installation:

```bash
crc version

```

### Step 4: Configure the System

Run the setup command to configure your host OS. This handles group permissions, networking interfaces, and virtualization settings.

```bash
crc setup

```

> **Note:** If the setup prompts you to log out and log back in to apply group permissions, please do so before proceeding to Step 5.

### Step 5: Start the Cluster

Launch the OpenShift instance using the pull secret you downloaded in Step 2.

```bash
crc start -p ~/Downloads/pull-secret.txt

```

*Estimated time: 10-15 minutes depending on hardware.*

### Step 6: Access Your Cluster

Once the terminal displays **"Started the OpenShift cluster"**, you can access it via the web console or CLI.

#### Web Console

* **URL:** `https://console-openshift-console.apps-crc.testing`
* **Developer credentials:** `developer` / `developer`
* **Admin credentials:** `kubeadmin` / *(password printed in terminal output)*

Remote Access:
To add an OpenShift console link to a remote Mac's /etc/hosts file, you must map the console's fully qualified domain name (FQDN) to the IP address of your OpenShift cluster (e.g., node or load balancer) by editing the file with sudo privileges. 

Steps to add to /etc/hosts:
1. Open terminal on your Mac.
2. Run: sudo nano /etc/hosts
3. Add a line at the bottom: <SERVER_IP_ADDRESS> console-openshift-console.apps.<cluster_name>.<base_domain>.
4. Save and exit (Ctrl+O, Enter, Ctrl+X). 

Example Scenario (CodeReady Containers/Local):
If your remote IP is 192.168.1.50 and the app domain is apps-crc.testing, add:
192.168.1.50 console-openshift-console.apps-crc.testing
192.168.1.50 oauth-openshift.apps-crc.testing 

#### Command Line (`oc`)

Configure your shell environment to use the cached `oc` binary:

```bash
eval $(crc oc-env)

```

Login as administrator:

```bash
oc login -u kubeadmin -p <your-password> https://api.crc.testing:6443

```

---

## 🧹 Cleanup

To stop the cluster and reclaim resources:

```bash
crc stop

```

To delete the cluster entirely (resets data):

```bash
crc delete

```

---


```

```


