find (/root/86344/) -not -user root// find a directory
"   " >(/root/86344.ans)// write a full path name 
useradd (user86315)// create a new user
passwd -l (user86315)// lock a password
openssl dgst -verify// obtain a hash value and check each public key
echo (Carol) > (/root/86302.ans)// write the answer in a file
losetup -f /(5d3a8e1b)// control, manage loop devices and set up devices. maps regular files to /dev/loop(0-9) nodes
cryptsetup luks0pen /dev/loop0 loop
mount /dev/mapper/loop /mnt
ls /mnt
cp /mnt/070f (/root)// copy the content of a filesystem to a directory
cp -r /mnt/lost+found/ /root
openssl (aes-128-cbc) -d -in (/root/86261.enc) -K (86261) -iv (0)// decrypt a file with key and initialisation vector
cat (/root/86261.txt)
openssl (des-ede) -d -in (/root/86257.enc) -k (86257)// decrypt a file using password and des-ede algorithm
umask 077 
cat >k //and copy private key
openssl dgst -sign k -sha256 -in (/root/86257.txt) -out (/root/86247.sign)// sign a file with the private key, use SHA 256 hash function and save the signature



