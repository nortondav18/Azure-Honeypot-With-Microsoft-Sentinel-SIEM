# Azure-Honeypot-With-Microsoft-Sentinel-SIEM
In this project I Deploy a public-facing Windows VM on Azure.
Intentionally expose certain ports (RDP) to attract malicious traffic.
Use Log Analytics and Microsoft Sentinel to collect and analyze attack logs.
Create KQL queries, custom alerts, and a Sentinel dashboard showing attack sources, geolocations, and methods.

<br><br>
Start off by creating a resource group this will be the container that holds all our resources for this project.
<img width="975" height="521" alt="image" src="https://github.com/user-attachments/assets/58132339-063e-446a-8e6a-044e856234f2" />

Create a virtual network and select your resource group. This is what provides our VM with internet access.
<img width="975" height="873" alt="image" src="https://github.com/user-attachments/assets/cdfc7442-3b75-4831-ad09-f69f377dea3b" />

Create a virtual machine and select your resource group.
<img width="956" height="872" alt="image" src="https://github.com/user-attachments/assets/a5a8f215-4c8d-4adc-9d76-87f1b8acbed9" />
<img width="855" height="932" alt="image" src="https://github.com/user-attachments/assets/ac16af0b-5d9d-48da-8a9d-44ee6893fe93" />

Go to the resource group and select the network security group. 
<img width="1214" height="773" alt="image" src="https://github.com/user-attachments/assets/6b3876de-0468-44f9-a6dc-b3d3a176a7fe" />

Delete the RDP rule.
<img width="1892" height="674" alt="image" src="https://github.com/user-attachments/assets/42c7cbc3-71df-464e-821f-a5b5844b502f" />


Create a new inbound security rule.
<img width="1890" height="887" alt="image" src="https://github.com/user-attachments/assets/c25a3407-0b53-4822-b1ff-5b25448e241c" />
<img width="867" height="491" alt="image" src="https://github.com/user-attachments/assets/c117ef61-100d-4dd2-82b7-50e516c32415" />


<img width="1310" height="737" alt="image" src="https://github.com/user-attachments/assets/66b29c64-f883-4a30-a57f-c2ac079726ba" />

<img width="1868" height="690" alt="image" src="https://github.com/user-attachments/assets/b3667307-744a-44de-8bb8-98a66a40a001" />

<img width="899" height="650" alt="image" src="https://github.com/user-attachments/assets/d6c7f489-1554-491b-89fe-d66007604f2f" />


<img width="1750" height="575" alt="image" src="https://github.com/user-attachments/assets/5f7f9fe6-736b-4c31-903a-9de0ef7ad8c6" />

<img width="1391" height="796" alt="image" src="https://github.com/user-attachments/assets/004f3e3b-de72-4e47-8efe-059963246998" />

<img width="1623" height="886" alt="image" src="https://github.com/user-attachments/assets/a3bf7d77-1b97-466f-8d56-62485ba4721c" />

<img width="1869" height="922" alt="image" src="https://github.com/user-attachments/assets/8b991a9b-2434-4775-b3b9-9b24f85f55e5" />

<img width="1899" height="934" alt="image" src="https://github.com/user-attachments/assets/016695f2-1bd9-4238-807b-ad2bfc9ab5e4" />

<img width="603" height="519" alt="image" src="https://github.com/user-attachments/assets/e7eb3f54-c1d1-4a3e-a9d9-5a50f8070dc7" />

<img width="1672" height="607" alt="image" src="https://github.com/user-attachments/assets/b8cf947f-6419-4ecb-b8c1-ef317e3904a6" />

<img width="1708" height="711" alt="image" src="https://github.com/user-attachments/assets/69f5fb71-2d2e-4213-97c3-bbcd363ba6ee" />

<img width="2510" height="1206" alt="image" src="https://github.com/user-attachments/assets/1e84dee1-542c-4956-92ac-7c4b899f9c39" />

<img width="1761" height="1214" alt="image" src="https://github.com/user-attachments/assets/775de5b4-c499-457b-9bae-9a0aeb197a45" />

<img width="2052" height="1112" alt="image" src="https://github.com/user-attachments/assets/405c3641-8d0f-43e4-b9d9-5c907aea18be" />

<img width="1459" height="514" alt="image" src="https://github.com/user-attachments/assets/a98ca9df-70a0-4d40-ac91-48df61b497a7" />

<img width="1550" height="885" alt="image" src="https://github.com/user-attachments/assets/e717c9a2-040a-492b-a673-36ba809012e0" />

<img width="1521" height="636" alt="image" src="https://github.com/user-attachments/assets/f6df4802-1f97-42f1-a6c2-479c8427b59e" />

<img width="2511" height="1118" alt="image" src="https://github.com/user-attachments/assets/f0262c53-1780-41c7-b485-52f5adb765e9" />

<img width="2511" height="1170" alt="image" src="https://github.com/user-attachments/assets/c18b4096-12db-4fcd-879e-2424733d3750" />

<img width="2159" height="597" alt="image" src="https://github.com/user-attachments/assets/df3d050b-c7ae-4b97-bd4d-f1b35b980945" />
<img width="1306" height="461" alt="image" src="https://github.com/user-attachments/assets/b1f9d7f8-9d58-42b9-a720-032e1b54bc6d" />










