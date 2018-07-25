# Create a machine on Azure



1. **Create a virtual machine in azure with Ubuntu 16.04**
   1. [**https://portal.azure.com/\#create/Canonical.UbuntuServer1604LTS-ARM**](https://portal.azure.com/#create/Canonical.UbuntuServer1604LTS-ARM)
   2. **Name: yourName**
   3. **Disk type: ssd**
   4. **Username: ubuntu**
   5. **Copy paste the result of \`cat ~/.ssh/id\_rsa.pub\` into ssh key textarea**
   6. **Leave the other defaults alone**
   7. **Resource group &gt; use existing &gt; bnext-staging**
   8. **Location &gt; South India**
      1. **Other locations will not have some key presets configured so selecting something like Southeast Asia will mean extra configuration that’s not documented here at the moment.**
2. **Size**
   1. **Choose: Standard DS1\_v2 \(1 vcpus, 3.5 GB memory\)\(search if not visible\)**
   2. **There are other options but they might be overkill**
      1. **Standard F4s \(4 vcpus, 8 GB memory\)**
      2. **Standard DS2\_v2 \(2 vcpus, 7 GB memory\)**
3. **Disk Size &gt; 128**
   1. **Select public inbound ports: HTTP, HTTPS, SSH**
4. **Map the new IP to FQDN via cloudflare \(use dns-only setting\).** 

