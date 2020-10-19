# Procedures for MGHPCC Shutdown #

### Unity Cluster ###

#### Power Down ####
1. Block access from the Palo firewall rule.
1. Shutdown all Compute Nodes
1. Shutdown the containers/VMs running on the head node in this order:
  1. Licensing Container
  1. Web VM
  1. Slurm VM
  1. Login Container
  1. NFS-gw VM
  1. Identity Container
1. Shutdown head node
1. Shutdown NAS1
1. Shutdown astro-th NAS
1. Shutdown cee-water NAS
1. Shutdown VAST
  1. Deactivate the cluster. This can be done by clicking on the cluster in the VMS UI maintenance page and hitting pause/deactivate or using VCLI (cluster deactivate) to do the same. Wait until the entire cluster deactivates cleanly on its own.
  1. Run these on any cnode to initiate shutdown. Cnodes shut down first, followed by Dnodes.
  ```
  #verify clush is healthy
  clush -a hostname
  #shutdown the cluster
  clush -g cnodes 'sudo /usr/sbin/shutdown -h +2'; clush -g dnodes 'sudo /usr/sbin/shutdown -h +5'
  ```
  1. Physically unplug power - the nodes come up automatically with power restoration

#### Power Up ####
1. Power up VAST
  1. Plug in in the D-nodes and wait for them to power up. Wait 10 minutes to ensure the D-nodes start cleanly.
  1. Plug in the C-nodes and wait for them to power up. Wait 10 minutes to ensure the C-nodes start cleanly.
  1. From the web UI, activate the cluster.
1. Power up cee-water NAS
1. Power up astro-th NAS in person, IPMI not yet set up
1. Poewr up NAS1
1. Power up head node
1. Power up head node VMs/containers
  1. Identity Container
  1. NFS-gw VM
  1. Login Container
  1. Slurm VM
  1. Web VM
  1. Licensing Container
1. Power up all compute nodes
1. Allow access from Palo Alto

### Perirhinal ###

#### Power Down ####
1. Pause all active VMs
1. Shutdown from Web UI

#### Power Up ####
1. Power up in-person, IPMI is not available

### CloudLab / OCT ###

#### Power Down ####
1. Power down head node

#### Power Up ####
1. Power up head node

### General ###
1. After the above, shut down the PA-3220