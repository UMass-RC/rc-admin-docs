# MGHPCC Annual Shutdown #

!!! note
    Items in *italics* should be done in-person

## Unity Cluster ##

### Power Down ###
1. Block access from Palo Alto
1. Shutdown all Compute Nodes from MAAS
1. Shutdown the containers/VMs running on the head node in this order:
    1. Licensing LXC
    1. Web VM
    1. Login LXC
    1. Slurm VM
    1. NFS-GW VM
1. Shutdown all NAS serving devices (excluding VAST)
1. Shutdown VAST
    1. Deactivate the cluster. This can be done by clicking on the cluster in the VMS UI maintenance page and hitting pause/deactivate or using VCLI (cluster deactivate) to do the same. Wait until the entire cluster deactivates cleanly on its own.
    1. Connect to any cnode via ssh (web UI ip, username: `vastdata`, pass: `vastdata`), and run these commands:
    ```
    #verify clush is healthy
    clush -a hostname
    #shutdown the cluster
    clush -g cnodes 'sudo /usr/sbin/shutdown -h +2'; clush -g dnodes 'sudo /usr/sbin/shutdown -h +5'
    ```
    1. *Disconnect power to the cnodes and dnodes, either in-person or through remote access to the PDU.*
1. Shutdown identity LXC on head node
1. Shutdown head node

### Power Up ###
1. Power up head node
1. Power up identity container
1. Power up VAST
    1. *Plug in in the D-nodes and wait for them to power up. Wait 10 minutes to ensure the D-nodes start cleanly.*
    1. *Plug in the C-nodes and wait for them to power up. Wait 10 minutes to ensure the C-nodes start cleanly.*
    1. From the web UI, activate the cluster.
1. Power up head node
1. Power up all NAS devices
1. Power up head node VMs/containers in this order:
    1. NFS-gw VM
    1. Login Container
    1. Slurm VM
    1. Web VM
    1. Licensing Container
1. Power up all compute nodes from MAAS
1. Allow access from Palo Alto

## Perirhinal ##

### Power Down ###
1. Pause all active VMs
1. Shutdown from Web UI

### Power Up ###
1. *Power up in-person, IPMI is not available*

## CloudLab / OCT ##

### Power Down ###
1. Power down head node

### Power Up ###
1. Power up head node

## Pikes ##

### Power Down ###
1. From CMGUI, power down all compute nodes
1. From CMGUI, power down head node, you will lose connection to Bright

### Power Up ###
1. *Power up head node in-person*
1. Power up compute nodes from CMGUI