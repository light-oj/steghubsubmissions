## Implementing LAMP Stack on Azure

### Introduction

Azure, Microsoft's cloud computing platform, offers a wide range of services that enable users to deploy and manage various applications and workloads. Implementing a LAMP (Linux, Apache, MySQL, PHP/Python/Perl) stack on Azure is a straightforward process that involves leveraging Azure's virtual machines (VMs), databases, and networking capabilities.

### Steps to Implement LAMP Stack on Azure

1. **Create a Virtual Machine (VM):**
   - Log in to the Azure Portal and navigate to the Virtual Machines section.
   - Click on "Create" to start the VM creation process.
   - Choose a Linux distribution (e.g., Ubuntu, CentOS) as the operating system for your VM.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/9a294502-820d-403f-856b-24c4ed12e28f)
   - - Configure the VM size, networking settings, and authentication (SSH key or password).
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/c2c61bee-e6e7-4632-a013-3634936de0c8)
   - Once the VM is provisioned, connect to it using SSH.

2. **Install Apache:**
   - Update the package repository on the VM using the package manager (e.g., apt for Ubuntu, yum for CentOS).
   - Install the Apache web server package.
   - Start the Apache service and enable it to start on boot.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/7e6b73db-6212-4ca3-8f87-e110a5dc2169)
   - Test Apache by accessing the VM's public IP address in a web browser.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/9f0a1d54-5056-43ac-90d0-288a59d24110)


3. **Install MySQL:**
   - Install the MySQL server package using the package manager.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/66eded0f-9a60-404a-91d4-67af0903d7ef)
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/c730eceb-b5da-4a44-bc01-26089a69b663)
   - Secure MySQL installation by running the security script (optional but recommended).
   - Start the MySQL service and enable it to start on boot.
   - Access the MySQL command-line interface to create databases, users, and grant permissions as needed.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/2837c422-2f33-4b7a-9b58-e50e5c010aeb)


4. **Install PHP/Python/Perl:**
   - Install the appropriate runtime environment for your chosen programming language (e.g., PHP for LAMP).
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/6bb761c4-9192-4c9e-b6da-70c2080f9e0c)
   - Test PHP installation by creating a simple PHP file and accessing it via the web server.
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/716eaad3-87d2-4977-8389-f52a0a3b297e)
   - ![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/ce1e0b4d-428b-4423-a012-f2689ce37b61)


![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/09964a1d-6e98-4812-be3e-be2c491a90ba)
![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/a07550dd-3755-478e-bb41-1f5df3dc52df)
![image](https://github.com/light-oj/steghubsubmissions/assets/46436281/e7ab2ec6-180c-481a-9d0f-cb62f088d92f)




