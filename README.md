# GlusterfsAWS

GlusterFS on Amazon Web Services

Gluster is general purpose scalable, distributed network attached storage (NAS) file system solution that aggregates EBS volumes across multiple EC2 instances into a single high performance resilient namespace. It gives horizontal scaling and provides high availability through replications within Amazon Machine Images (AMI).

Installation of Gluster in Amazon Web Services on Linux. 
Gluster1

 ![Image](https://github.com/user-attachments/assets/588ed9a2-86d5-4e93-9646-8fedb86441fd)
 
Gluster2

 ![Image](https://github.com/user-attachments/assets/4ddd6bb0-54f2-4852-8be2-2d5960ddbea5)
 
Client 

![Image](https://github.com/user-attachments/assets/21075755-3a19-432b-b750-fce5116e535d)

I did some prerequisites first doing an update then installing the server on the nodes in the linux machine using these commands. sudo apt-get install software-properties-common, and sudo add-apt-repository ppa:gluster/glusterfs-5. That would get the repositories then apt update then install by doing apt install glusterfs-server and enable it too start after boot by adding systemctl enable glusterd. Then on the client machines I did apt-get install software-properties-common, and add-apt-repository ppa:gluster/glusterfs-5 commands then updated the client system apt install glusterfs-client command. 
 
![Image](https://github.com/user-attachments/assets/88fd23a8-381f-49c3-a7b1-78ccbd417c89)

![Image](https://github.com/user-attachments/assets/0c0f4971-6da6-42b9-be81-bc2bce18acc3)

![Image](https://github.com/user-attachments/assets/8f77fc79-946f-41d6-a1e4-9b4feff9aac3)

![Image](https://github.com/user-attachments/assets/840c3ec5-3d0c-4744-885c-7a2001cb1807)

Did an update to ensure everything is up to date

![Image](https://github.com/user-attachments/assets/a9d259e4-38da-4cae-8d47-4b12fc49ebf0)

Configure Firewall & GlusterFS Trusted Pool
If UFW is running, run the command below to allow the storage nodes to communicate with each other.
sudo ufw allow from <other-node-IP>. To create a trusted storage pool between the nodes, run the probe from Storage Node01 as shown below;
gluster peer probe gluster1 (I did the same for gluster2)

![Image](https://github.com/user-attachments/assets/68045aa8-7203-42f5-b59d-7eb3379102f3)

![Image](https://github.com/user-attachments/assets/b6e82f03-c18b-4bab-a5bf-0df5ed150593)

![Image](https://github.com/user-attachments/assets/495ca529-9630-4311-9b9e-c741f5875c53)

![Image](https://github.com/user-attachments/assets/9d484ead-c3f7-49dc-8108-91d082bf0399)

Configure GlusterFS Trusted Pool
To check the status of the trusted pool just created above, execute the command below;
gluster peer status

![Image](https://github.com/user-attachments/assets/a4c853ed-928e-4456-aac6-2c1f7a3c8b53)

![Image](https://github.com/user-attachments/assets/d3c949e6-3bc8-457d-abb5-e137fd41d463)

To list the storage pools ill use the gluster pool list command

![Image](https://github.com/user-attachments/assets/3a87fb8a-9af1-408a-a86b-eea3ca69ad4b)

![Image](https://github.com/user-attachments/assets/7e03a861-0a3d-40a6-b9ed-dda7322d7072)

Create Distributed GlusterFS Volume
I created a brick directory for GlusterFS volumes on the GlusterFS storage device mount point on both storage nodes. mkdir /gfsvolume/gv0

![Image](https://github.com/user-attachments/assets/ca09ddb0-8ab6-4ee5-8550-9bbc8fe29c06)

Next, created a distributed volume called distributed_vol on both nodes using the command
gluster volume create distributed_vol transport tcp u18svrnode01:/gfsvolume/gv0 u18svrnode02:/gfsvolume/gv0

![Image](https://github.com/user-attachments/assets/5b698a31-cd1f-4c97-bdcd-a462fedfc034)

Then to start the created volume I did gluster volume start distributed_vol     

![Image](https://github.com/user-attachments/assets/6869094e-22f9-43b5-a9f3-0991c87b9d84)

![Image](https://github.com/user-attachments/assets/bba059a3-130e-42ce-af33-c66fb91c496a)

To show my information about the created volume. gluster volume info

![Image](https://github.com/user-attachments/assets/53c43042-74af-4718-8eee-05ee5abded71)

![Image](https://github.com/user-attachments/assets/650e4a97-c21f-469a-b188-2bd4d0f3bb6f)

Mount the volume on GlusterFS client
Create the mount point first with mkdir /mnt/gfsvol. Then mount the distributed volume using the command mount -t glusterfs u18svrnode01.example.com:/distributed_vol /mnt/gfsvol/. After I ran the df command to check the mounted filesystems by typing df -hTP /mnt/gfsvol/

![Image](https://github.com/user-attachments/assets/f347ab4d-dc02-4b5a-87bd-52b589ea6d30)

 

 
 

 
 

 
 

 
 

 
 

 
 

 

 
 

 

 
 

 
