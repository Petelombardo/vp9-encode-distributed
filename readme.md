This script allows you to use several PCs or VMs or Containers to distribute the load of transcoding a video to VP9/Opus format.<br>
Input: Varies<br>
Output: VP9 + Opus<br>
It is intended to copy 5.1 channel audio and up to 1080i video.  It will automatically deinterlace the video if needed.<br>
<br>
REQUIREMENTS<br>
<li>Either shared storage (preferred) for the video processing, or a copy of the video in the same location on each system</li>
<li>Linux with ffmpeg installed on each system</li>
<li>libvpx installed</li>
<br>
INSTRUCTIONS
<li>Run ssh-keygen on all of the nodes</li>
<li>Copy vp9-encode-distributed to one of the servers in the cluster.  That will be your master node as well as a worker node.</li>
<li>Make the script executable by running: chmod a+x vp9-encode-distributed.</li>
<li>Run ssh-copy-id from the master node (the one with this script) to all other nodes</li>
<li>Mount a share in the same mount point on each worker node.  You can use NFS, or if you do not have common storage, just use sshfs to mount.</li>
<br>
Examples:<br>
<br>
Login to server1<br>
wget https://raw.githubusercontent.com/Petelombardo/vp9-encode-distributed/master/vp9-encode-distributed<br>
chmod a+x vp9-encode-distributed<br>
Edit the script and set the variable SERVERS="server1 server2".<br>
ssh-keygen<br>
ssh-copy-id server2<br>
ssh server2 "sshfs root@server1:/mnt/shared /mnt/shared"; # Mount server1's /mnt/shared folder on server2<br>
./vp9-encode-distributed /mnt/shared/movie.ts benchmark;  # Run this only the first time, or if your server list changes<br>
./vp9-encode-distributed /mnt/shared/movie.ts; # This kicks off the actual vp9 encoding<br>
./vp9-encode-distributed /mnt/shared/movie.ts status; # Tells you the current status of all of the systems.<br>
watch bash ./vp9-encode-distributed /mnt/shared/movie.ts status; # Keeps the status of all of the systems up on your screen perpetually.  ctl-c to stop it.<br>
./vp9-encode-distributed /mnt/shared/movie.ts join; # Run this after encoding completes on all nodes.  Give the complete path+filename when prompted.  example:  /mnt/movies/movie.mkv<br>

