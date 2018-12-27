Copy vp9-encode-distributed to one of the servers in the cluster.  That will be your control node as well as a worker node.
Make the script executable by running: chmod a+x vp9-encode-distributed.
Mount a share in the same mount point on each worker node.  You can use NFS, or if you do not have common storage, just use sshfs to mount.

Examples:

./vp9-encode-distributed /mnt/shared/movie.ts benchmark;  #  You only need to run this once so that it knows how to distribute the load
./vp9-encode-distributed /mnt/shared/movie.ts; # This kicks off the actual vp9 encoding
./vp9-encode-distributed /mnt/shared/movie.ts status; # You can run this as many times as you want.  A status of 1 = 1st pass done.  Status of 2 = 2nd pass done (i.e. encoding complete).

