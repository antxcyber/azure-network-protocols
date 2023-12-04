<p align="center">
<img width="100" alt="Screenshot " src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/d1b92d2d-52dd-4036-bd01-72145fb4449f" height="100" width="15%" />

</p>

<h1 align = "center">Virtual Machine Network in Microsoft Azure</h1>
This tutorial outlines how to set up an Virtual Machine Network in Microsoft Azure and doing some exercises observing traffic.

<br />

<h2>Environments and Technologies Used</h2>

<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Microsoft Remote Desktop</li>
  <li>Windows Command Prompt</li>
  <li>Wireshark</li>
  <li>Network Protocols</li>
  <ul>
    <li>DNS - Domain Name System</li>
    <li>ICMP - Internet Control Message Protocol</li>
    <li>SSH - Secure Shell</li>
    <li>RDP - Remote Desktop Protocol</li>
  </ul>
</ul>

</br>

<h2>Operating Systems Used </h2>
<ul>
  <li>Windows 10 (21H2)</li>
  <li>Linux (Ubuntu 20.04)</li>
</ul>

</br>

<h2>List of Prerequisites</h2>
<ol>
  <li>Microsoft Azure Account and Subscription</li>
  <li>Access to Microsoft Remote Desktop Connection</li>
  <ul>
    <li>For MacOS users, follow <a href = "https://www.youtube.com/watch?v=0lllpAhgAJs&ab_channel=TheHostingVideos">this video</a> to use Remote Desktop on Mac</li>
  </ul>
  <li>(OPTIONAL): Notepad for typing down log in information for our Virtual Machines</li>
</ol>

<h2>Installation Steps</h2>

<h3>Creating our Resource Group and Virtual Machines</h3>

<p>
  <ul>
    <li><b>Resource Group</b></li>
      <ul>
       <li>Through <b>Azure Services</b>, go to <b>Resource groups</b> to create a Resource Group and name your Resource Group <b>RG-VM</b>. Take note of the <b>Region</b> of your Resouce Group as it'll come in play when setting up our VMs. Once done, then click on <b>Review + Create</b></li>
        <ul>
          <li> <img width="736" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/801d9846-ec7f-477a-ba0d-b69d3ec6f5dc">
</li>
        </ul>
      </ul>
    <li><b>Virtual Machine 1 using Windows 10</b></li>
    <ul>
      <li>Through <b>Azure Services</b>, go to <b>Virtual Machines</b> to create an Azure Virtual Machine. Select the Resource group we've created (RG-VM) and name the virtual machine <b>VM-1</b>. Make sure the <b>Region</b> is the same as your Resource Group and we'll set our <b>Availability Options</b> set to <i>No infrastructure</i> and <b>Security Type</b> to <i>Standard</i> for this tutorial</li>
      <li>Set the <b>Image</b> (our Operating System) to <i>Windows 10 Pro, Version 22H2, x64 Gen2</i></li>
      <li>The <b>Size</b> selected dicates the general processing power and RAM of our VM, for this tutorial we'll set it to <i>Standard_E2s_V3</i> which provides 2 virtual CPUs and 16 GBs of RAM</li>
      <ul>
        <li> <img width="736" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/2185fab9-dcb1-44d6-b700-ba69e6145c7d">
</li>
      </ul>
      <li>Set the username and password of your VM for logging in and make sure to check the box for licensing agreement</li>
      <ul>
        <li> <img width="733" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/d261f8ee-8fc3-4170-bf78-7fa79e4690cc">
</li>
      </ul>
      <li>Go to the <b>Network</b> tab and notice the <b>Virtual Network</b> created by the Virtual Machine as it should've been made by the Resource Group. It will be made automatically by the Virtual Machine</li>
      <ul>
        <li> <img width="733" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/f0b4b91a-0ab8-4d25-bd64-37ca17515316">
</li>
      </ul>
      <li>Then head to the <b>Review + Create</b> and click on <b>Create</b> to deploy your Virtual Machine. Give it some time to fully deploy before moving on.</li>
    </ul>
    <li><b>Virtual Machine 2 using Ubuntu</b></li>
    <ul>
      <li>Same process as Virtual Machine 1 but we'll name the VM <b>VM-2</b> and set the Image to <i>Ubuntu Server 20.04 LTS x64 Gen2</i></li>
      <li>Ubuntu by default has their Administrator Account authentication as SSH public key, so we must set it as Password for logging in through Remote Desktop</li>
      <ul>
        <li> <img width="733" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/63e20f29-7209-4f40-8e39-119e84afce2b">
</li>
      </ul>
    </ul>
  </ul>
</p>

<br />

<h3>Logging into a Virtual Machine using Remote Desktop Connection</h3>

<p>
  <ul>
   <li>Through <b>Azure Services</b>, go to <b>Virtual Machines</b> and select VM-1 we've created and click on <b>Connect</b> to connect to the VM, from this page you can obtain the <b>Public IP Address</b> which we will use to connect to it via Remote Desktop Connection</li>
    <ul>
      <li> <img width="762" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/24420832-956a-4be0-a963-968604f20fca">
>
</li>
    </ul>
    <li>Copy the address and paste it into Remote Desktop Connection and click on <b>Connect</b> and log in using the username and password you set up for VM-1 (a pop up may show up for verification, just click on "Yes" if it does)</li>
    <ul>
      <li> <img width="755" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/8fbca3af-da2b-415d-bf85-31a7ca1b08c7">
</li>
    </ul>
    <li>You are now successfully logged into your VM!</li>
    <ul>
      <li> <img width="755" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/26158869-feef-4779-bb73-7100ad434546">
</li>
    </ul>
  </ul>
</p>

<br />

<h2>Observing Traffic in Virtual Machines</h2>

<h3>Download and Install Wireshark</h3>

<p>
  <ul>
    <li>First, download <a href="https://www.wireshark.org/download.html">Wireshark</a> in your VM. Downloads may be slow depending on your VM's CPU</li>
  </ul>
</p>

<br />

<h3>Observing ICMP (Internet Control Message Protocol) Traffic</h3>

<p>
  <ul>
    <li>Once installed, open Wireshark and start capturing packets (the blue fin icon). In the filter bar, type <b>icmp</b> to filter incoming ICMP packets</li>
    <ul>
      <li> <img width="753" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/8e4a2dec-80d5-43fa-9bc0-1f8d9d2a7467">
</li>
    </ul>
    <li>Back to your physical desktop, head to your Microsoft Azure Account obtain the <b>Private IP Address</b> of VM-2 and copy it</li>
    <ul>
    <li> <img width="478" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/1267cbad-93ac-4ebe-8c4f-8b1c28635001">
</li>
    </ul>
    <li>Open up <b>Windows Powershell</b> in VM-1 and in the command line enter <b>ping</b> and the private IP of VM-2. Once done, ICMP packets should now display in Wireshark</li>
    <ul>
    <li> <img width="756" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/d14ec304-ed6e-45fa-bc3b-07c89a2eac0a">
</li>
    </ul>
    <li>We will now start a perpetual / non-stop ping between the Virtual Machines by entering <b>ping</b> then the private IP of VM-2 followed by <b>-t</b> causing nonstop ICMP packets displaying in Wireshark</li>
    <ul>
    <li> <img width="756" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/ea3fbe88-3147-4413-91fd-07daf6a0622a">
</li>
    </ul>
    <li>Heading back to the Microsoft Azure Account, we'll go to the VM-2's <b>Network Security Group (NSG)</b> (which should be named <i>VM-2-nsg</i>) in order to halt the traffic</li>
    <li>In VM-2-nsg, we'll go to <b>inbound security rules</b> and create a security rule that denies ICMPs. Click on <b>Add</b> to open a right side pop up to set the rule and dot in <b>Deny</b> under action and <b>ICMP</b> under Protocol. Set the Priority higher than 300 (priorities are inversely proportional meaning lower numbers have higher priority) and name the rule <b>DENY_ICMP_PING</b> then click <b>Add</b> to finish</li>
    <ul>
    <li> <img width="756" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/426314dd-519f-463e-9f95-70f4427123ee">
</li>
    </ul>
    <li>Once completed, you'll notice the message "Request timed out" will start displaying in Powershell in VM-1, meaning ICMP ping has been halted from our security rule</li>
    <ul><img width="692" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/b9a08d23-e818-4b7a-9dff-5a963b2d19cd">
    <li>To reinstate the traffic, simply head back to your Microsoft Azure Account and set the DENY_ICMP_PING inbound rule's action to <b>Allow</b> and save</li>
  </ul>
</p>

<br />

<h3>Observing SSH (Secure Shell) Traffic</h3>

<p>
<ul>
  <li>In Windows Powershell inside VM-1, type in <b>ssh VM-2@[VM-2's Private IP]</b> then hit Enter, enter in "yes" and it will ask for the password for VM-2</li>
  <li>Since we are accessing the Terminal of VM-2 (essentially Linux's version of a command prompt) it doesn't diplay input/dots when typing a password but do know it is registering input when typing</li>
  <li>Once logged in, you will be connected to the Terminal of VM-2. You can exit by entering the command <b>exit</b></li>
  <ul>
  <li><img width="733" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/8ba636b4-92b9-4c71-b2f3-8d909bcd3559">
</li>
  </ul>
  <li>Typing in commands such as <i>username, pwd, or sudo apt</i> will display traffic on Wireshark, you can filter ssh traffic in Wireshark by typing in <b>ssh</b> in the filter bar</li>
</ul>
</p>

<br />

<h3>Observing DNS (Domain Name System) Traffic</h3>

<p>
  <ul>
    <li>Filter DNS traffic in Wireshark by entering <b>dns</b> in the filter bar</li>
    <li>In Powershell, type in <b>nslookup</b> and a website such as google.com</li>
  </ul>
</p>

<br/>

<h3>Observing RDP (Remote Desktop Protocol) Traffic</h3>

<p>
  <ul>
    <li>Filter RDP traffic in Wireshark by entering <b>dns</b> in the filter bar and you'll notice non-stop traffic</li>
    <li>This is because the RDP is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted</li>
  </ul>
</p>

<br/>

<h2>Clean Up</h2>
<ul>
  <li>Log off Remote Desktop Connection</li>
  <li>It is advise to delete your Resource Group and VMs after finishing tinkering with them to prevent future costs, deletion of assets on Azure require verification by entering the name of the asset. Also to note, the Resource Group <b>NetworkWatcherRG</b> is created when creating NSGs for Virutal Machines and requires its own deletion</li>
  <ul>
  <li><img width="735" alt="image" src="https://github.com/antxcyber/azure-network-protocols/assets/148983947/7de064b2-286d-45eb-bd9a-276a7417f476">
</li>
  </ul>
</ul>
