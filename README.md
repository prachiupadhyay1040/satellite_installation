# satellite_installation

 


Verifying DNS resolution 

Using below COmmands 

ping -c1 localhost 

ping -c1 `hostname -f` # my_system.domain.com 

 

Note -  

To avoid discrepancies with static and transient host names, set all the host names on the system by entering the following command 

hostnamectl set-hostname name 

 

Configuring Satellite Procedure 

Disable all repositories: 

subscription-manager repos --disable "*" 

Enable the following repositories: 

subscription-manager repos \ 

--enable=rhel-9-for-x86_64-baseos-rpms \ 

--enable=rhel-9-for-x86_64-appstream-rpms \ 

--enable=satellite-6.16-for-rhel-9-x86_64-rpms \ 

--enable=satellite-maintenance-6.16-for-rhel-9-x86_64-rpms 

 

Verify that the required repositories are enabled: 

dnf repolist enabled 

Installing fapolicyd on Satellite Server 

You can install fapolicyd along with Satellite Server or can be installed on an existing Satellite Server. If you are installing fapolicyd along with the new Satellite Server, the installation process will detect the fapolicyd in your Red Hat Enterprise Linux host and deploy the Satellite Server rules automatically. 

Prerequisites 

Ensure your host has access to the BaseOS repositories of Red Hat Enterprise Linux. 

Procedure 

For a new installation, install fapolicyd: 

dnf install fapolicyd 

For an existing installation, install fapolicyd using satellite-maintain packages install: 

satellite-maintain packages install fapolicyd 

Start the fapolicyd service: 

systemctl enable --now fapolicyd 

Verification 

Verify that the fapolicyd service is running correctly: 

systemctl status fapolicyd 

 

Installing Satellite Server packages 

Procedure 

Update all packages: 

dnf upgrade 

Install Satellite Server packages: 

dnf install satellite 

Configuring Satellite Server 

Install Satellite Server by using the satellite-installer installation script. 

 

Procedure 

Enter the following command with any additional options that you want to use: 

satellite-installer --scenario satellite  

--foreman-initial-organization "NIC"  

--foreman-initial-location "Pune"  

--foreman-initial-admin-username admin 

--foreman-initial-admin-password “xxxxxxx” 

Note - The script displays its progress and writes logs to /var/log/foreman-installer/satellite.log 

 
