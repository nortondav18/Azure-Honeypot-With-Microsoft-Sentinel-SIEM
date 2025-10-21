# Azure Honeypot With Microsoft Sentinel SIEM
In this project I deploy a public facing Windows VM on Azure.
Intentionally expose certain ports to attract malicious traffic.
Use Log Analytics and Microsoft Sentinel to collect and analyze attack logs.
Create KQL queries, a Sentinel dashboard showing attack sources, and geolocations.

<br><br>
Start off by creating a resource group this will be the container that holds all our resources for this project.
<img width="975" height="521" alt="image" src="https://github.com/user-attachments/assets/58132339-063e-446a-8e6a-044e856234f2" />

Create a virtual network and select your resource group. This is what will provide our VM with internet access.
<img width="975" height="873" alt="image" src="https://github.com/user-attachments/assets/cdfc7442-3b75-4831-ad09-f69f377dea3b" />

Create a virtual machine and select your resource group and network group.
<img width="956" height="872" alt="image" src="https://github.com/user-attachments/assets/a5a8f215-4c8d-4adc-9d76-87f1b8acbed9" />
<img width="855" height="932" alt="image" src="https://github.com/user-attachments/assets/ac16af0b-5d9d-48da-8a9d-44ee6893fe93" />

Go to the resource group and select the network security group. 
<img width="1214" height="773" alt="image" src="https://github.com/user-attachments/assets/6b3876de-0468-44f9-a6dc-b3d3a176a7fe" />

Delete the RDP rule. Deleting the specific RDP rule and then creating a new rule that allows all inbound traffic is done to make the honeypot appear as wide open and “vulnerable” as possible.
<img width="1892" height="674" alt="image" src="https://github.com/user-attachments/assets/42c7cbc3-71df-464e-821f-a5b5844b502f" />

Create a new inbound security rule and set the destination port to '*'.
<img width="1890" height="887" alt="image" src="https://github.com/user-attachments/assets/c25a3407-0b53-4822-b1ff-5b25448e241c" />

Conect to your VM using the credentials you just made.
<img width="867" height="491" alt="image" src="https://github.com/user-attachments/assets/c117ef61-100d-4dd2-82b7-50e516c32415" />

Once you login go to the firewall settings and turn off the firewall. The reason we do this is because the Windows firewall on your Azure VM blocks inbound traffic by default, which prevents most scans or exploit attempts from reaching your services.<br>
The Network Security Group acts like a perimeter firewall at the Azure network level it controls what traffic is allowed to reach the VM.
But inside the VM, the Windows Firewall still decides whether to accept or reject that traffic.

So even if your NSG allows all inbound traffic the Windows Firewall might still block: RDP (3389) SMB (445) HTTP (80) or any other service
That means your honeypot would look “dead” or unresponsive to attackers. They could connect to the IP, but every port would appear closed.<br>
Turning Off the Firewall Makes the Honeypot Fully Open

By disabling the Windows Firewall:

All inbound traffic that the NSG allows can actually reach the operating system.

Attackers can attempt logins, scans, and exploits on any service/port.

The system starts generating rich logs (failed logins, process creation events, Defender alerts, etc.).

Essentially, this makes your honeypot visible, vulnerable, and valuable for analysis.


<img width="1310" height="737" alt="image" src="https://github.com/user-attachments/assets/66b29c64-f883-4a30-a57f-c2ac079726ba" />

Try to ping the VM you should receive replies meaning the VM is exposed to the internet.
<img width="1868" height="690" alt="image" src="https://github.com/user-attachments/assets/b3667307-744a-44de-8bb8-98a66a40a001" />

Create a log analytics workspace so that we can colect and query logs from our VM remotely.
<img width="899" height="650" alt="image" src="https://github.com/user-attachments/assets/d6c7f489-1554-491b-89fe-d66007604f2f" />

Search for Microsoft Sentinel in the search bar, create and add your log analytics workspace.
<img width="1750" height="575" alt="image" src="https://github.com/user-attachments/assets/5f7f9fe6-736b-4c31-903a-9de0ef7ad8c6" />

Go to the content hub in Microsoft Sentinel.
<img width="1391" height="796" alt="image" src="https://github.com/user-attachments/assets/004f3e3b-de72-4e47-8efe-059963246998" />

Install the Windows Security Events solution and click manage.
<img width="1623" height="886" alt="image" src="https://github.com/user-attachments/assets/a3bf7d77-1b97-466f-8d56-62485ba4721c" />

Select Windows Security Events via AMA. This will allow us to ingest security events from the VM.
<img width="1869" height="922" alt="image" src="https://github.com/user-attachments/assets/8b991a9b-2434-4775-b3b9-9b24f85f55e5" />

Create a data collection rule.
<img width="1899" height="934" alt="image" src="https://github.com/user-attachments/assets/016695f2-1bd9-4238-807b-ad2bfc9ab5e4" />

Select your VM and create.<br>
<img width="603" height="519" alt="image" src="https://github.com/user-attachments/assets/e7eb3f54-c1d1-4a3e-a9d9-5a50f8070dc7" />

Go back to your VM and go to extentions + applications then select the data collection rule.
<img width="1672" height="607" alt="image" src="https://github.com/user-attachments/assets/b8cf947f-6419-4ecb-b8c1-ef317e3904a6" />

now go to the log analytics workspace and select logs. Senteniel uses KQL which is very similar to SQL. Start by searching for all security events. You will likely need to let the VM run for a few hours to collect some logs.
<img width="1708" height="711" alt="image" src="https://github.com/user-attachments/assets/69f5fb71-2d2e-4213-97c3-bbcd363ba6ee" />

Here we search for invaild login attempts and there is quite a lot.
<img width="2510" height="1206" alt="image" src="https://github.com/user-attachments/assets/1e84dee1-542c-4956-92ac-7c4b899f9c39" />

We can refine our search so we only get the informaion that we are interested in.
<img width="1761" height="1214" alt="image" src="https://github.com/user-attachments/assets/775de5b4-c499-457b-9bae-9a0aeb197a45" />

From here we can look up where these invaild login attempts are coming from to help determine if they are malicous, if it isnt't already obvious.
<img width="2052" height="1112" alt="image" src="https://github.com/user-attachments/assets/405c3641-8d0f-43e4-b9d9-5c907aea18be" />

We can query all sort of differnt event IDs and monitor our VM. 
Here I search for event ID 4720: A user account was created to see if any new account were created.
You could also query event ID 4624 to see if any attacker was able to gain access to the VM.
<img width="1459" height="514" alt="image" src="https://github.com/user-attachments/assets/a98ca9df-70a0-4d40-ac91-48df61b497a7" />

Now lets create a Workbook in Sentinel.
A Workbook in Microsoft Sentinel is used to visualize, analyze, and monitor security data. Essentially, it turns raw log data into meaningful dashboards and insights.
<img width="1550" height="885" alt="image" src="https://github.com/user-attachments/assets/e717c9a2-040a-492b-a673-36ba809012e0" />
<img width="1521" height="636" alt="image" src="https://github.com/user-attachments/assets/f6df4802-1f97-42f1-a6c2-479c8427b59e" />

To start I query for a count of top 10 IP address that are failing to login to the VM
<img width="2511" height="1118" alt="image" src="https://github.com/user-attachments/assets/f0262c53-1780-41c7-b485-52f5adb765e9" />

I further refine the query so that it displays the contries names for the top attackers.
<img width="2159" height="597" alt="image" src="https://github.com/user-attachments/assets/df3d050b-c7ae-4b97-bd4d-f1b35b980945" />
<img width="1306" height="461" alt="image" src="https://github.com/user-attachments/assets/b1f9d7f8-9d58-42b9-a720-032e1b54bc6d" />

I also created a Workbook query that displays the timeline of when these invaild login attempts are happening.
<img width="2511" height="1170" alt="image" src="https://github.com/user-attachments/assets/c18b4096-12db-4fcd-879e-2424733d3750" />













