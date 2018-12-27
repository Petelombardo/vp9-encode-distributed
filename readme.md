This script allows you to use several PCs or VMs or Containers to distribute the load of transcoding a video to VP9/Opus format.<br>
It is intended to copy 5.1 channel audio and up to 1080i video.  It will automatically deinterlace the video if needed.<br>
<br>
INSTRUCTIONS<br>
<br>
Copy vp9-encode-distributed to one of the servers in the cluster.  That will be your control node as well as a worker node.<br>
Make the script executable by running: chmod a+x vp9-encode-distributed.<br>
Mount a share in the same mount point on each worker node.  You can use NFS, or if you do not have common storage, just use sshfs to mount.<br>
<br>
Examples:<br>
<br>
./vp9-encode-distributed /mnt/shared/movie.ts benchmark;  #  You only need to run this once so that it knows how to distribute the load<br>
./vp9-encode-distributed /mnt/shared/movie.ts; # This kicks off the actual vp9 encoding<br>
./vp9-encode-distributed /mnt/shared/movie.ts status; # You can run this as many times as you want.  A status of 1 = 1st pass done.  Status of 2 = 2nd pass done (i.e. encoding complete).<br>
./vp9-encode-distributed /mnt/shared/movie.ts join; # Run this after encoding completes on all nodes.  Give the complete path+filename when prompted.  example:  /mnt/movies/movie.mkv<br>

