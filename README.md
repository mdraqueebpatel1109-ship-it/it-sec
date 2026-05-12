# 1. Allow the owner of the private key to log in as root
# First, save the private key from the screen into a temporary file
cat <<EOF > /tmp/temp.key
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQCWKujUpBx1h6ye0
4lVLu8HEv11nRhNUHpMFabwhy57mEgZG704ZNZ+iVODxpjpbpEBE9DuksQnEH8+c
Xe8jrjiNF9huFKXMutkFLTrYFtd9PwUUN3admkpnOy28YsgFzhpnWP99KmZ85cmd
wNx6pzPhRMigDT+ljPGFGSRaipgnAgMBAAECgYEAtRAY0EUpff78LsbEFGAFERZ1
B31Nbj8MjtkaK4xt2GjfJJCFF0+PZmJP8pBznMfAwRXInSOsqMX9WfKLamyqlRqi
cp4RsT6TTLLWYkHUFIVYvTxQ1a6UbZ47l/3DM2wjLRV3+P/eaIBC+dyL4craH2H8
Kp8YvCrVKoc7tJWRqJECQQD6oDh1Yp9vdpCDIbFOAdcqpDynZi3rws1wILOwSXeP
oseE4bZFsJq80yG8aw3wmdy3U6HWBnzvRZAbYj5XTZgZAkeA1xonWEki8/HaaCH3
MVAuK+Vmo4jTaYvxv2Ah5oCqL8054aE4q+CrLCx4JbbfmrrzNL08qkwi/ZTdwr/V
63C6PwJARZ+Iz6NMI0zOrH8JoGAhAQIDYDNnN1y8LlELhxagH5R6upBfm8PKZiT
3mj3AGXd2NfU17bHYbjzZYgPRXV60QJBALaW1dUkaA4p05tvUZTDmvcpCKJC8Crl
BzXLVZuDlnNrMotrvl5wHP8nVmm1PUPR8+zFsZ3heUZGkqRZES6FByMCQQCmhSh8
eBQSEUnoJmuMKZ7TuqhGNAV3d8/DYJ5gzv1aPYyaa9Aaa/kQis3l8jdu2id8Ytc3
iF1ru9f4uTQfh6Rs
-----END PRIVATE KEY-----
EOF

# Extract public key and append to root's authorized_keys
mkdir -p /root/.ssh
ssh-keygen -y -f /tmp/temp.key >> /root/.ssh/authorized_keys
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
rm /tmp/temp.key

# 2. Remove files in /root/d203589/ not owned by root
find /root/d203589/ -type f ! -user root -delete

# 3. Set account expiration for user203590 to 2025-01-01
usermod -e 2025-01-01 user203590

# 4. Identify which file matches the signature, then run these checks to see which one returns "Verified OK"
openssl dgst -sha256 -verify /tmp/pub.key -signature /root/203591.sign /root/203591A.txt
openssl dgst -sha256 -verify /tmp/pub.key -signature /root/203591.sign /root/203591B.txt
openssl dgst -sha256 -verify /tmp/pub.key -signature /root/203591.sign /root/203591C.txt
echo Anne(name) > /root/203591.ans

Alternative way-
for name in Anne Bob Carol Daniel Eve; do
    echo -n "Checking $name: "
    openssl dgst -sha256 -verify /root/${name}-86302.pub.pem -signature /root/contract-86302.sha256.signature /root/contract-86302.txt
done

# 5. Create the user160184 user and generate a new default ssh RSA key (/home/user160184/.ssh/id_rsa) for it without passphrase. Allows user160184 to log as root with the help of the RSA private key
useradd -m user160184
-u user160184 ssh-keygen -t rsa -b 4096 -f /home/user160184/.ssh/id_rsa -N ""
chmod 700 /root/.ssh
cat /home/user160184/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys
chmod 600 /root/.ssh/authorized_keys

# 6. Find the directory in /root/160171/, in which the sticky bit is set. Write the full path name to the file: /root/160171.ans
find /root/160171/ -type d -perm /1000 > /root/160171.ans

# 7. Account expiration for user(1/1/25)
chage -E 2025-01-01

Configure the user account operator so that its password expires on 2021-07-24 and its maximum number of days between password change is 100-
chage -E 2021-07-24 -M 100 operator

# 8. Download the file e3fae9a2 with the help of the command below. curl -o /e3fae9a2 https://progcont.hu/docs/IT-S. The file contains an encrypted filesystem in LUKS format. The password is e3fae9a2. Copy the content of the filesystem to the directory: /root
curl -o /e3fae9a2 https://progcont.hu/docs/IT-S
echo "e3fae9a2" | cryptsetup luksOpen /e3fae9a2 temp_volume
mkdir -p /mnt/temp_mount
mount /dev/mapper/temp_volume /mnt/temp_mount
cp -r /mnt/temp_mount/* /root/
umount /mnt/temp_mount
cryptsetup luksClose temp_volume
rmdir /mnt/temp_mount

# 9. Set the permissions of the file /root/160101.txt so that its permissions show as -r--rws--T in the directory listing 
chmod 3460 /root/160101.txt

# 10. Remove all privilege-related entries (ACLs) and restrict access
setfacl -b /root/199299.key
chmod 000 /root/199299.key

# 11. Set ownership of the file /root/160076.txt so that the owner will be operator and the owner group will be users
chown operator:users /root/160076.txt

# 12. Copy the first 70 byte of the file /root/160067.dat to the file /root/160067.part
dd if=/root/160067.dat of=/root/160067.part bs=1 count=70

# 13. Generate an 1024 bit RSA key and save it as /root/160060.pem as a PKCS8 private key 
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:1024 -out /root/160060.pem

# 14. Create a new crypto_LUKS encrypted xfs filesystem on /dev/sdc and mount it to the /mnt directory 
cryptsetup luksFormat /dev/sdc
cryptsetup open /dev/sdc crypt_sdc
mkfs.xfs /dev/mapper/crypt_sdc
mount /dev/mapper/crypt_sdc /mnt

# 15. Create a self-signed certificate for self.my-factory.eu
openssl req -x509 -newkey rsa:4096 -keyout /root/self.my-factory.eu.key -out /root/self.my-factory.eu.crt -days 365 -nodes -subj "/CN=self.my-factory.eu"

# 16. Decrypt the file using AES-128-CBC
openssl enc -aes-128-cbc -d -in /root/199301.enc -out /root/199301.txt -K 33333333333333334444444444444444 -iv b0b0b0b0b0b0b0b0b0b0b0b0b0b0b0b0

# 17. Find /root/199302/ directory not owned by root and write path to .ans file
find /root/199302/ -type d ! -user root > /root/199302.ans

# 18. Open LUKS filesystem, mount it, and copy contents
echo "cbnyr" | cryptsetup luksOpen /root/199304 my_encrypted_volume
mkdir -p /mnt/temp_luks
mount /dev/mapper/my_encrypted_volume /mnt/temp_luks
cp -r /mnt/temp_luks/* /root/
umount /mnt/temp_luks
cryptsetup luksClose my_encrypted_volume

# 19. Set owner of the file to operator
chown operator /root/199305.txt

# 20. Give read-only permissions to operator via USER ACL
setfacl -m u:operator:r /root/199306.txt

# 21. Create new user and lock the password
useradd user86315
passwd -l user86315

# 22. Decrypt the /root/86257.enc file by using the 86257 password and the des-ede algorithm. Save the result as /root/86257.txt 
openssl enc -des-ede -d -in /root/86257.enc -out /root/86257.txt -pass pass:86257

# 23. Sign the /root/86247.txt file with the following private key. Use the SHA 256 hash function. Save the signature as /root/86247.sign!
cat <<EOF > /tmp/private.key
(key)
EOF
openssl dgst -sha256 -sign /tmp/private.key -out /root/86247.sign /root/86247.txt
rm /tmp/private.key

# 24. Set the permissions of the /root/86237.txt file to read-only
chmod 444 /root/86237.txt

# 25. Create a file with name /root/86198.dat and with a size of 861980 bytes
dd if=/dev/zero of=/root/86198.dat bs=1 count=861980

# 26. Create a new /dev/sdc1 partition on the drive /dev/sdc. Format the partition with ext2 filesystem and mount it to the /mnt folder in read-only mode
printf "n\np\n1\n\n\nw\n" | fdisk /dev/sdc
mkfs.ext2 /dev/sdc1
mkdir -p /mnt
mount -o ro /dev/sdc1 /mnt

# 27. Add IPv4 subnet to firewalld home zone permanently
firewall-cmd --permanent --zone=home --add-source=10.250.250.0/24
firewall-cmd --reload






