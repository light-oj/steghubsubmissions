### Web solution with Wordpress

##### Step 1 - Prepare a Web server

To prepare a web server:

1.  Launch an EC2 instance that will server as “Web Server”. Create 3 volumes in the same AZ as your web server EC2, each of 10GB.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdX1Ta-DlXKfiJ2QhpMnCbCBJFcZcmxDOsECsaCyBSz3Q-LRDiBaIURkBvEzaBJrvvenoyyACkXySEf3MyPj8f1fpxs6G3q6Of66Tdbitquk4JO5VNk-Ks-K_JHi0G7WwHUegs7l8u_UDHVpd5loGnsLqZV?key=-AmqoHU_JCb21FYvySdS_g)

To add EBS volume to EC2 instance, navigate to Volumes in left blade. Click on Volumes and then create volumes.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe-uIbYzeyRVkPjB_2-zWOtQ8_KZ_rcyK-ZcMQU1E8VNzdVogOk9qR0Mc3MUK-OW4kZ-HBPcpYxU4d2Zu8c9XceCsuK5o9--MctUOjrMgd3OeEYjmFh4XJS-qbddt1zQS3Vw3ATASIXxNCS5BPUirVmaE4?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXegPHI-cssB1dglwefAgZvOh_fciHJDvQNN8UExW5V1xWC3MU3E0oz_-xUHszToCA1_Urbi7XHlCxmmCdO0hqwpTYw2TGShNhbsIAeA0cg9WEZaXGB2EOcA91ZJGaxO46zEnASMCk1zwHH7mMUqVw9lUnc?key=-AmqoHU_JCb21FYvySdS_g)

2.  After creating the volumes, attach all three volumes one by one to the web server EC2 instance.

Right click on each instance and attach volume

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXewAjXRriKtB0j97HTLW1r8REIZU1e6f8juGapVpqe9Yr6rxPJPBsfFBIfMEZOY1q_4icndSHDNJo7a2LYKBL3_15BnZt4nh8joWfRj9Da1cCW-fNMSNv4M6qIcAHND1DxT16lJne6sSDkHQtvOPHqOpUic?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfh-8LuOqHdLXUqWDF0k8yO5iA-eT5Bqc31spyqnyMwpLPHeWQpnOvX0WhTSnTPeVIiIqQMz9FPojWugfO52kHNvuBhpuLgmF8kwJkzOloZiyyZAHYWgAm451UCBTLpjW9bgOL2UFJThFcrpEetOs1sKI6N?key=-AmqoHU_JCb21FYvySdS_g)

3.  Connect to the Linux terminal to begin configuration

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeV8SHFdS9W7FukeJ2AFxiAzJopRFdsztfHPQ8UlEVzSx79LgcnqRogMbbgKWVivOAw_5qivIo_5Rw-XegvXJkbPuxwNG4pc28O_aGn3B3HjVj5K6-buQxFNrjP2pEPJJW3KCApnErd8kaynddQQBwax7FM?key=-AmqoHU_JCb21FYvySdS_g)

4.  Use `lsblk` command to inspect what block devices are attached to the server. Notice the names of the newly created devices. All devices in linux resides in /dev/ directory. Inspect with ls /dev/ and make sure you see all 3 newly created block devices there - their names will likely be xvdb, xdvc, xvdd

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXelPB9wBzLpLlzHdpypzlzmr6086DNVp8DRPBRH3llgqA7n2iRjIQSMWSnho_t50ShdkWEfadsrnPvI2pwfPpsd2WKDviksawfte6kjSyj0FPkmsZ5zsMzkNt7IJ8J8rRAFBcuyHum2j0VBEZvGylqp118u?key=-AmqoHU_JCb21FYvySdS_g)

5.  Use `df -h` command to see all mounts and free space on the server.![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcW0r8n1dbQ5oK9b3bDvHfQysvmxb4ysFiYjUO1IYgq55mEnTkcmVLiqFO93ztdR-TSUxrlQVlgx-HoE0QH5fyl6AjKzblfgJjvI1yaZLS3C08fbHpXnqsXGHrYQ9KMBbKm5Zsm7BN70LtLBAjKez06gkw?key=-AmqoHU_JCb21FYvySdS_g)
6.  Use `gdisk` utility to create a single partition on each of the 3 disks.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeSAO1nSh01dcYigxyEsMub8PuwgNmbXN49SHvHpDmF3ZUQHunnxlT3UBnbOdEvDfL085ihl8FNjv30rt-j8aiYmgzczcuPdo8711KvSCOWEXlsaYtPLPI-M8uPkEvTvWhH8H2lLG1NTCXB9kLzV17Zo_w?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe-e3HDxm6Q7InToT6AfW5pfLUEGghec3LTQ_00n-NfuwHiypXjnvaDTDAhtD7nYcYZlqQ7g-yU3i3wUOsj-ym1Hzze6vYqj2d-EJ1tqKdDpTPDrsEjNedJ3CqMYFz7eCCg3muXp7yqi86YPwWKg9uLhOcA?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdQGz7s9qSBxy6OGu6d8C7YMV93MSt64NRew2oU7huKP62JjCAUbBldiHLJYbFe9QoiUswhEBDnhAD2zgReNUfHpAtVDP81AZxN5MIjM13IzzmaS3CuQIPS2QBbazfHNf6MvI9WMjnsrH7RLyFY3W1vYhw?key=-AmqoHU_JCb21FYvySdS_g)

7.  Use `lsblk` utility to view the newly configured partition on each of the 3 disks

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcaqevAZVRY_1uZl92gUqIwKs0O2j4-CJQ_vRDKckBc-H_spLq-mUoNijOl9RbGWpdySNDjs9QrCBgzbWM2gaWZB4TWfICyu4ncqSIlH30vJFZ9EEOZ7j2Ea9YjZeHrwL-RnEkqxz_yeCyVYzaArG6gNvzB?key=-AmqoHU_JCb21FYvySdS_g)

8.  Install lvm2 package using `sudo yum install lvm2`. Run `sudo lvmdiskscan` command to check for available partitions.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcMAHfYaFkYTPQi258iHEwBdUd8cPb9fQs8hEjFECXbEFuug-987bHssKq4wTC9YsR2eiA34hqlfJoibneTzPvTVnqoAMpEKvZJVxktXNSnpaJmS3I5FFw5_ycN1xnkSrlGJgM36xggFsju9BEehDsB4cOv?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdZ7SG9RcKxHgZ4g6lLH6c4jUxzfyS6GEVQ_NfKHSDtVi7wWW1IfVJYSO0A3_8JdqgNLlakhRNJblIQ8zz8fpcRqyEa23EUxycf8Zn0hV8XT_cnj88UqrHb0zZij-YUxC0UsePWQH5KaCs48wyOXCeLqfyA?key=-AmqoHU_JCb21FYvySdS_g)

9.  Use `pvccreate` utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcAp22BcpIHkK9iPnoDoi7C7POsQr4canwDrclyYfjoSjrDWITSa9zBtcWqukdWXAseH8L_x2wkC7oyTvTnJCsCKMfApqXqWJ4bXeWVpxY2VZQCSRB1Pk6IS3dEALhBv99PK8XfaJKX9dZtoC3zvg0CB7cp?key=-AmqoHU_JCb21FYvySdS_g)

10.  Verify that the physical volumes has been created successfully by running `sudo pvs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeDtmd7YuaZ6rmB4eLFrXHgipJfG-Mwb95hQJKUBylD-xESzHPTWlsi_8uvXyl5VAOvp_zwEfCDOLWkUG48wi80O1rfmLbM0eqOMLcrHcTZIMo9s6qGtNMLeSJw3iDC-e8E1CxXFcMoWGxqeBjZ0kcnfpfT?key=-AmqoHU_JCb21FYvySdS_g)

11.  Use `vgcreate` utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeOZqmR9-0vCZ3bncIyAI96EcF0TZc_voDd-HmptggJYI9xXBM6-qb7WRf1JkEIbABF24vbC9Ww1Z6pJJD0iFLeHZN7rPqSMqHfOHLXivFW0aEKc6pscP_9ybLTN-zxflA3FqYqqOqcIUDtnC2W2jKJddyW?key=-AmqoHU_JCb21FYvySdS_g)

12.  Verify that the VG has been created successfully by running `sudo vgs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeAutuVZ4DCUU15mUOScMU9_LI4mawGeOlUhGbSkGdSpv_WqRsqVOXM4P4-9qOjCJNUH7yMt2k89fc4XO0OyegsI_ejKDjZ78lIJ3io-PdWbsq2PCC13M1aNH_7PQ-liDOblaIfftA7aAK56-vSR2P3ht-K?key=-AmqoHU_JCb21FYvySdS_g)

13.  Use `lvcreate` utility to create 2 logical volumes apps-lv (Use half of the PV size) and logs-lv (Use the remaining space of the PV size). Note: apps-lv will be used to store dta for the website while logs-lv will be used to store data for logs.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfZMMaXDuCAotEsChIwod2avxzgizurxfUWtoggY6gqTe_FyDknQ67SS-URERDbwYLGnKKeYusWwsKovEWRbxM5a5U2bGrsxkr_49V5T4V4hmtcRJn86lG66zp_ywMl7TJ315y1BLvZ4C-DMuFz1G6Ndijr?key=-AmqoHU_JCb21FYvySdS_g)

14.  Verify that the Logical Volume has been created successfully by running `sudo lvs`

 ![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeNPxeMQTbwh7BXGoi0Bs5x132SkUdBN4tz5pOAOW46uQJUNsTsqKOidbByDMAiYwmdwTj6vtD75mxqA2BQx52xX6phZoJVljOqlEs2KppVvikQFsr9ZwyuwUjsO1sV9JQmjCseRDZPc4FWJHKziyZmh9GM?key=-AmqoHU_JCb21FYvySdS_g)

15.  Let’s verify the entire setup

`sudo vgdisplay -v #view complete setup -VG, PV, and LV`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdNTUg9q0b-NI3zLtztuNpk-UC0YiIKFGCQny4tQ_eej-INJrBRGBaluWDSpMvBCxBvVSxkVAeBFqCE6sr0dlem3qF-vMDQGpZ5JccMXlOijdJIr6iHSnHLYh3vlvZbD6KJvL5ONHP61IUC20EKWQlpHrTG?key=-AmqoHU_JCb21FYvySdS_g)

`sudo lsblk`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXckPwv9vLaY6r_VDtpTrLa3hnikZQyVlYWWTk-gRghSWzvVFN6bcZViI8QiyxEDr7_WwyrtWY9DLkoljtNSBw_IW6N39PLiSAsOLVD0-WpIo6RTJx5HgS8ArXX9Ymddb6_sIQ-UfsYRC5vVMbhtByGoosSm?key=-AmqoHU_JCb21FYvySdS_g)

16.  Use `mkfs.ext4` to format the logical volumes with ext4 filesystem

`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`

`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfj1rhIi997GPcfUaApaYQ95xzNauNivDL5IYYZjdNMjU7cXYB42ANYFuaPaijXkqchEpLpXUi_jlkyKGqI4OBdZahrmx2Oh78Bgncaj8jCF26or9hSioMdN_Cjpbmwxn0uMzF_zlMlt6o5YIiPHOdAU8Tf?key=-AmqoHU_JCb21FYvySdS_g)

17.  Create /var/www/html directory to store website file `sudo mkdir -p /var/www/html`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe0z-wieevC50MW8FV672KroMMdMW-yRAZHcCNiaIk9Y8c36H7McHUTN8pPw2PcIBdsknNOyKSYpBkMy4HafzJN4fQBAE-oE5Z_lk2pdqZarXIQ3CE1uvukDb9UzFSWlR40b7Zsb-tRmHW4juozkDV62Rua?key=-AmqoHU_JCb21FYvySdS_g)

18.  Create /home/recovery/logs to store backup of log data `sudo mkdir -p /home/recovery/logs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfc0jU-hVwfBxcqc6E_oC9ZybKtRK8De1U-JUJMHH-YAG6jSP8XMfvPrIE_s1yKKUUWeKErGRj7HaWZDLKIsFaajRZ-F8YpjzI2FcVanC-PHq-_OAJK6Hs67LpoaNRFmP3CqOvyXxJ2wpjE074LPBIj4aY?key=-AmqoHU_JCb21FYvySdS_g)

19.  Mount /var/www/html on apps-lv logical volume

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfa_PvhUMZ3gwu6ZMPO0b5VKiOlGPGdzJ2rquuVbjJ8r0IB8AYXU-3bKHsYwpI7WnWB3u5PZOF8cTrzpDv1o-Fhyt59_WuslnkOfZ9wj3TF3SLXj_gj9JjgKTJopy9R6IDzXgpHpRWFdis565bvy9kI5V__?key=-AmqoHU_JCb21FYvySdS_g)

20.  Use `rsync` utility to backup all the files in the log directory /var/log into /home/recovery/logs (this is required before mounting the files system)

`sudo rsync -av /var/log/ /home/recovery/logs/`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcJTfbIGnY1yE3-l3YAis-_mqrNf9XwDQfJHe5U6dAYZ31KdGKJPBq0EKNcEWpGiT9UB-kd7CNWN_zyH8RI9ZS_R1CboMB9ixsIhyCarzvdGS-YnGF41nb81fP8e81HptuA-Ech2qLggGA2xv7C6vkRp0w?key=-AmqoHU_JCb21FYvySdS_g)

21.  Mount /var/log on logs-lv logical volume (Note that all existing data on /var/log will be deleted. That is why the step above is very important)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcgfXP6j8mhC941xuv18QEpc1QYR5yFlvkYO9zX4MOtf_pFNRLMdtThvB6tRg06yZOsy8t3IPKVqddVkcI0LRylhmjdEJxAe2RlNfC6tS4lVjqrRYxtUXCgyv2vJzAgtLUqsrXG7tN1S0un2ttDoLdAcDyv?key=-AmqoHU_JCb21FYvySdS_g)

22.  Restore log files back into /var/log directory

`sudo rsync -av /home/recovery/logs/ /var/log`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeMehYtnFEg0gwfhEridcfTOwn0ulaWc-k86THGSHXbp8zYHmgq5jAG-RumqdIkVhs7ZeZxg7q-4Pvpp06Yi1l2s_dmIO6F3P6E1heGM1t416cJfCnFDC7v38QRtCuigETyTusNJH-WJnRGk5Z1ZhOUVL6r?key=-AmqoHU_JCb21FYvySdS_g)

23.  Update the `/etc/fstab` file so that the mount configuration will persist after restart of the server.

The UUID of the device will be used to update the `/etc/fstab` file;

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcUSFQyUIXp45cZnBD4pBjrgGkM08BLu5kAhJXkA6dI_r-xH3YCn-FZXUBG8E_tqxPhpNvtuITNdXVfAlykguVsoEAlT1AaGl03QpOeaoPgD-zek1IrjsxfJ3jyk7gaIDhgiemTsc6owkd3Lzex97WnwN35?key=-AmqoHU_JCb21FYvySdS_g)


`sudo nano /etc/fstab`

Update `/etc/fstab` in the format below using your own UUID and remember to remove the leading and ending quotes.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXd8OyMiVtvkhZ-Mx7D9W4cfXy9aEFUrNZzSI5Z9GlsLVj3kuqU8paQDaSeLJ4GZDjDA8mYvCrfkq5llZRT5B0FFJr290Dj2uzZVjha77w7U6Ud-wmFm-KmvQiMkQ8S0Llx-I7hZ_XkRpfq6KWxCBIjrgRdu?key=-AmqoHU_JCb21FYvySdS_g)

24.  Test the configuration and reload the daemon

`sudo mount -a`

`sudo systemctl daemon-reload`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcvZqZTQsSq2yQEvDEFEopz3dNWCr-xuzQl2ACnWpU2LgJNqPlJvS63f_ypWyfO83Ff4TMl1IFgC3uRFTTzd6mKzy2PfrW6xxF7JXWm67dF_xwJyk0WWLrbXy2tef6V_f6V1MMuzuI3Ggtz4TkDPubiwAk?key=-AmqoHU_JCb21FYvySdS_g)

25.  Verify the setup by running `df -h`, output should look like below:

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdMKUQ_I1VGshCDw2Jrs0b2ePvpxW3S80-McbOm1cWkZzk1zRb7LsMO7q2ilS96bP1MJ5izEr9AnOrwzZUWolhHX-PKNhc8KATGRTLWtZSvsk7AF7iCe6lFrZegaVGnjED0wdYx3vII9fS1eoCkOMA9AMs?key=-AmqoHU_JCb21FYvySdS_g)

#### Step 2 - Prepare the Database Server

##### To prepare a web server:

1.  Launch an EC2 instance that will server as “Db Server”. Create 3 volumes in the same AZ as your database server EC2, each of 10GB.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdqiva_N1DZofpgXcONqTn9OYVbUvKSCcjiVhULa3CEsQM-iKAkJTTlfq-n2u3v70TSxmVQA8BIgt-Aw2qOn5VFbmwomFS9mKcSZWx_oUQ43MT1TnbDGZbDdBqNnvvQaPyztq__2bMwDn-0NkV6tk488pNZ?key=-AmqoHU_JCb21FYvySdS_g)

To add EBS volume to EC2 instance, navigate to Volumes in the left blade. Click on Volumes and then create volumes.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXflM0hydMMpsSjlk28D-cWJhUtcAw-RPj69K9st2BIKLza0tBt8cOrmGJXxlJPPTuwcB06C_PAwWJcqR7xzaQjGlQiDcSGpQb1DKdKLtfvzCViGMsH3qxlmPLmwFr6wPjyX8OrNO75NwiZfxoczhJHgQGQ?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdDlaRQMD06NMBdz7fYWy-lzB1il9R_EG3iHn4yNoF4XKz_W0xJXFoircoGQTOuMsg1IJTa31f34LIMSD57ChoiOJ0QtK1yUApE38RBuIDML6RarS6RuZSTJnBDSn2hiHGDFw-dSe1i2_TG0FIL-U_sVyvZ?key=-AmqoHU_JCb21FYvySdS_g)

2.  After creating the volumes, attach all three volumes one by one to the database server EC2 instance.

Right click on each instance and attach volume

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdiLNQNtzg0um9eDn_Dv2YiiAk-h-TTn10yZnhxRjuPuveKastn0JTPkpdu0yT6_90Lp0b0DC_wULhxg8UN5BmUUt7A5fkAUn_OK-xjdL6n3qZdi2tThN7FSKONPcE9g3kqkU-Axui1ef5Eh0QI70iuzAIu?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdlIH8zGYmzz4WcwJbofLQVjOXzdFUYEDd6eQXBKfgcI388r-hknWddk8aCX345iKfZKL2bnImFPNztfstmTJA4EytApRz9gjYRUfs66ssmSx5l2XEz-qV49wHYcitxeiw0j-nIdLkNUA3N_6eJcObdabUA?key=-AmqoHU_JCb21FYvySdS_g)

3.  Connect to the Linux terminal to begin configuration

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfc6esARIrp3cJxcVOYsZAtzGSqM1lcemSlPKxTXioWsiivE0ZdMWIO4j57eN3AOnj8yg-HeV64fnqtJCcNPG_pcpWaf25oKCdhq9wecoQ1vj__hVRsLLfQAXFHf01EPeg9556xj0Oek3v3yvHNoZvGsvCh?key=-AmqoHU_JCb21FYvySdS_g)

26.  Use `lsblk` command to inspect what block devices are attached to the server. Notice the names of the newly created devices. All devices in linux resides in /dev/ directory. Inspect with ls /dev/ and make sure you see all 3 newly created block devices there - their names will likely be xvdb, xdvc, xvdd

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXf4ftuzdcBWkuu0XnKaMatSZQZ8mdDbEXlVwZ71J87Rq8h0qxmC71lnDMjNb86SjHgDS50MkFHDY1Hpkxg3-OWYQuKbIMziwRo4OhOaUNwcxnNcF2pxibiDOyHlN68TmamSXB2bwa5Ywh5LM3S7qzQvro6U?key=-AmqoHU_JCb21FYvySdS_g)

27.  Use `df -h` command to see all mounts and free space on the server.![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdRolmIwJUtVm81wmMqV-eCjW1t7K_Ogw43l3BXReGcsy8ebv2hccvY6E5i8UYFUtGagnimDIg2xmF7GrLeZUNg19mY3cfK1tinT6Hlx-k5XnwLSQ8_9BD4xr9iHX9KPIejWn7wIA_p57gL7R72cnlTi6gP?key=-AmqoHU_JCb21FYvySdS_g)
28.  Use `gdisk` utility to create a single partition on each of the 3 disks.

`sudo gdisk /dev/xvdb`

`sudo gdisk /dev/xvdc`

`sudo gdisk /dev/xvdd`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcA_5i0DrwWZLTaSiDLSKisgeg7KMJc-e0wdzKJh87HkoFGvbkZMR4is94BZelcNNL-IxUnzgUOm5Y6uMzxu6hJlFD5qxfauL86vt3UIGCR4pJtTknibo1z9Lj1F-lUnyhzeAx6LUlGjYCNycjm785LgPyV?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeGRSX0jXhXJNDAKhR509ggziUnUP_lDQuCdmVhMJc6e0L2Ho4njenVV-u3vbgUMHLmjX4z1NRniyCD14do75g13byfbgT2TueA69-RFl1hW24YPAWTlpq0IKxUSNWTuYaUgH4eAmnM-koBlRjU6mKtbesX?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdHcxgd2yZIQLRaBGnW7glJTVWabuhmPwzLM4sMsaD3aG1HBmJyBt9U1mgZ_PcpG77zCLLU4-H_MP8ynOZ2r0lBOylcaqPs5E3irgYfqPYZJ23MuaVvO8G6Q8ZGmlJ3WqT92xSC-50W34MIgDwnzJLJryYt?key=-AmqoHU_JCb21FYvySdS_g)

29.  Use `lsblk` utility to view the newly configured partition on each of the 3 disks

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeieys307A_GbclYgrgtp34QHlKAd68tfFd_Z_6Iu50RXDjl5m3np7O56teP71GmXpdrUuc5IBhBCrGdiggurcYqP8B6fZwDYPP6Gg2swRBi8pUrHSy2Xg2x8c_6GveKaGc167qnG6Q0Ev2PN57tRHFBqE6?key=-AmqoHU_JCb21FYvySdS_g)

30.  Install lvm2 package using `sudo yum install lvm2`. Run `sudo lvmdiskscan` command to check for available partitions.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcUr8pPXORrTN2XWyHA9hYlZblfsm6BIvmPWvvoLNPlIBI6wc4MLTEVph2BGXlF8heX6LD6dQ6enbR8Ygc3r3vrO_HhfvtXYK_zG9rIxJo9QQfjxLK8HC8llRuL5LUwTZiVPnZSdLqlqqYFZNH1vaBkI4xU?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfZfTaMixAZvVmPKF1zsDg1Pjl8Mfq1L1r41n64vaItDnzhTP6pOixFSS0gEyKmAAdaRU8lf3LKYCBTMo-hcz4miozOYn9LFkeemoppCoLPPghN3OZqPsg4-GqmnMHFGc4ozkLHRnqsM346zn5FhX3OjMHQ?key=-AmqoHU_JCb21FYvySdS_g)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdC6FD6OMcBMxYfyGtGFuhLP1_8vqSMNE-SLl-fXXZ4mZ8ftxZaPxjm7J_CZfONCTkSPiEWgRr7okZuzeOp9iR9JlrZIQnpI0gxIJVnWoet-KDcz6mQW0-BVWEp95Qzh3FS6pNhdcbwRuOe0SIgZMVyVTj_?key=-AmqoHU_JCb21FYvySdS_g)

31.  Use \`pvccreate\` utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM.

`sudo pvcreate /dev/xvdb1`

`sudo pvcreate /dev/xvdc1`

`sudo pvcreate /dev/xvdd1`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcTK18KcJKKQ_zEFbk-zhCax4YOEvPFrh94ypNnllYCBtkfUhjdRpwk2Z0gXrKlzvmKqKyEZT9HFaRxovSsIdD28lKIAtiljohXIxe4t4b1KBzl4isrApc66VP3oUGyQRUj5oussyVcym7r4SiBDj3_a8hJ?key=-AmqoHU_JCb21FYvySdS_g)

32.  Verify that the physical volumes has been created successfully by running `sudo pvs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXelcF6EWpHMqg2r6lRbdKpgGPPppfuC8o3uZgd04FkMy3dLeWL_03uuWgTS9-1lCVxU_8m06SUbT3KZu3YKPVRUF05bTOg68tCb_xhK6449KmsoHRaOTxARmv3FKYImnGFpTGvggV23QuPTkUa2YbHoYORL?key=-AmqoHU_JCb21FYvySdS_g)

33.  Use `vgcreate` utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg

`sudo vgcreate webdata-vg /dev/xvdd1 /dev/xvdc1 /dev/xvdb1`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXd_LX_9NKiMZ9GlyMrMhGAjf8ImMUO6aoPFBtim-_eAgyhHDJsNLyA_E-MPgnXVis8_B36ReO6jFbfNpTecqfjKUJS7BZysKDN2BkmwIBoCsPw7SAW-KsoJV8Oob35Qy0NqWDGpREM_ZzKdcQK6cg0msUaG?key=-AmqoHU_JCb21FYvySdS_g)

34.  Verify that the VG has been created successfully by running `sudo vgs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcsEDTkHpxVFfKfoKCi-hLRFyHyyIl6BZf1LA6SiURZu5IrSHDlHOkCT1AdT9sFS4y_tSfHb9-fkQytxf_EOsIXyTBb6c5mbR5rHBN_LJP-6yJx-sxGgfBcYelJadSMfYb7k6z9LIjG72bs4FCpr-j7CTY?key=-AmqoHU_JCb21FYvySdS_g)

35.  Use `lvcreate` utility to create 2 logical volumes db-lv (Use half of the PV size) and logs-lv (Use the remaining space of the PV size). Note: apps-lv will be used to store data for the database while logs-lv will be used to store data for logs.

`sudo lvcreate -n db-lv -L 14G webdata-vg`

`sudo lvcreate -n logs-lv -L 14G webdata-vg`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXetDVFOVWaQuBDb4UwS-JCdwOdRcRWBSQ55mzxdgKuRCzsZCjnRcoTFR9AJMrncNbJ5hzHq7LJuMwDwGco25aac-QDJ15Rw4fiQ7oEymsyJiYeVGAjIGZfdlxVMJ_tlYbOTUoA102Q0C5O-bYstNS-9xyL6?key=-AmqoHU_JCb21FYvySdS_g)

36.  Verify that the Logical Volume has been created successfully by running `sudo lvs`

 ![](https://lh7-us.googleusercontent.com/docsz/AD_4nXc9QXgB-Iei3Q0dLg_cGfckivXkZ3ieacbsQVCWiRTh9rUOxFQRbq05_6gzH2NP9-P5-NrMXJjbTfBZeTcNKo1Hr8tuOCbzq8tqArQ-N3eZIX3gO82SM9eZs6WE_JmFET311pXeWaNbVcYTnEk4RbNabEhQ?key=-AmqoHU_JCb21FYvySdS_g)

37.  Let’s verify the entire setup

`sudo vgdisplay -v #view complete setup -VG, PV, and LV`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdiSfODPAdnn2R8nmVl9EB5SVrT5wm3otsMH5Pb9c5Shu1xvqWA2g_Lnh8hPuIVy172CaloHnHFD7aS7eZATru2HmFk9zkDgvUeMkolFsknrgkir60zaGoEtblndgxjqF_6AJ034roYkTEvmMk6-hSsHnhw?key=-AmqoHU_JCb21FYvySdS_g)

`sudo lsblk`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfnvAxspV8OJDnjfdbimKEeQiRrKhEhWcWllF_se57G-n6RudHeIS1lGp5SvjubNAhtTV9muPBMGmZsCEzdimKnFPRpHOX1s97aHd_FVLjCQtBeVpIZJpXlTFJq-4qRkem3wWT9uqQJoBdVsU85gnJ5Pkw?key=-AmqoHU_JCb21FYvySdS_g)

38.  Use `mkfs.ext4` to format the logical volumes with ext4 filesystem

`sudo mkfs -t ext4 /dev/webdata-vg/db-lv`

`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeGZcwi2CPFAQ58EtvL8PVjucsM5k0jbNDLZawX8srMZWEcWPjtXS8KvVdEooyp6polEarP3bW3Ss0NCylulaX4dgdgRFM3UjkkqH0sdxw9e9GQ-Zul4VLsW9hXPptABDSgY4kartTCmKRS-SOMg5svO5M?key=-AmqoHU_JCb21FYvySdS_g)

39.  Create /var/www/html directory to store website file `sudo mkdir -p /db`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXdz2oPbTHSGHG-Enpql9uswUZrvbvyrxDSS-JFCNQeR4JKNbSy3H7C6JvUMpmwyolxqy5yK71wgifz_Ll5WNp90OGkXdvwuVcnfqqkzcTZkVagTRMHTr_PxolRRD68hKnh1gS4X-5ADP__BArpHuLaYoPTw?key=-AmqoHU_JCb21FYvySdS_g)

40.  Create /home/recovery/logs to store backup of log data `sudo mkdir -p /home/recovery/logs`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeNxvKSkwWa67BFcZYtlJiwm5qqqEusPYgOBWYe3Y8NGH_49U2BQXjXCZJiSAlcw9Z9WjY80TCWGohdCY-fJP22PtU562JH5_cSmmbO5zi6r9Rs0voheay3NMoiU9TQmhx71M7ywa4C5BElY03-5jKjYWC6?key=-AmqoHU_JCb21FYvySdS_g)

41.  Mount /db on db-lv logical volume

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXc-kRrClSnPQb9wARD52BTP9pcO-TPiMA2fdNpjhLoSGa_8ZaT4ZeSd0dkvRVXmj_7SBZWOMJoRkjQpoY1DjNDTj-erDTt1FFVaVC_XI-uA8G2lutCuMSKMqsjkp7vzJtV3LBoKX8FGL7E0t1ZMJ6eLRhgZ?key=-AmqoHU_JCb21FYvySdS_g)

42.  Use `rsync` utility to backup all the files in the log directory /var/log into /home/recovery/logs (this is required before mounting the files system)

`sudo rsync -av /var/log/ /home/recovery/logs/`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcxbV9_4JrtfdyXANEc6Zi-agjAIJSCABLDYWjlNR5bQJ5pM5b5cwLtzeqOH6e-_gh0aVI6gwB-Iyq81UsC18znT2UFZVSCspMB3-MUTPBF6HZ-Q4PNl1qSUY-fAU93LsQGnTcyYxGLJfq0ISGJtmtso0U?key=-AmqoHU_JCb21FYvySdS_g)

43.  Mount /var/log on logs-lv logical volume (Note that all existing data on /var/log will be deleted. That is why the step above is very important)

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXczvjnN-pyDft71KCb-3iZpsHvHcoFBeO4jrQ5ueeESs4Fdev079v5Kth40HKqb4uX-ALfXvFEAbCGegmvmlcRD1SadzPooVRg9tamS5ykclZJpyPqTct7-vin6G6Nqz_LGOmrA-rs_QOBUz2blTh5wVg?key=-AmqoHU_JCb21FYvySdS_g)

44.  Restore log files back into /var/log directory

`sudo rsync -av /home/recovery/logs/ /var/log`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeQ3CxqZiZVB7D40rWr7SQExOFXW_gpLxKV7x1lQkFiPLXY7SHtQnSGywsGWuGGQBRsSF8fcnkx-0XR7jyCr7Q6DoD9SQ1alrwPnblsG_FLYh10gR8nhibZFAJoDPsMP_GpY33dCC3f7txwlDUnS8DkkQ7m?key=-AmqoHU_JCb21FYvySdS_g)

45.  Update the `/etc/fstab` file so that the mount configuration will persist after restart of the server.

The UUID of the device will be used to update the `/etc/fstab` file;

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXcUSFQyUIXp45cZnBD4pBjrgGkM08BLu5kAhJXkA6dI_r-xH3YCn-FZXUBG8E_tqxPhpNvtuITNdXVfAlykguVsoEAlT1AaGl03QpOeaoPgD-zek1IrjsxfJ3jyk7gaIDhgiemTsc6owkd3Lzex97WnwN35?key=-AmqoHU_JCb21FYvySdS_g)

`sudo nano /etc/fstab`

Update `/etc/fstab` in the format below using your own UUID and remember to remove the leading and ending quotes.

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXeYDn6-NyENQjrMY2z0v--u6rFz93kX6hPJLP50OuhjLtjtRyUZ572MfyeWgMR2iZ7IjDcE9OMDOuzeGjwk4mVglsJIm2EyjkCh0Ap34wNE1m9vgOqgD7kb-G5uEOhaImx8tBGrSInMBxRrs6h7SiOm9G60?key=-AmqoHU_JCb21FYvySdS_g)

46.  Test the configuration and reload the daemon

`sudo mount -a`

`sudo systemctl daemon-reload`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXfnzd1IgX6yDfMrcoVKhBWe2DSbSNsAf2vUQzQdBdskoLynujXaXlM30rKlNYZTmm_egn6lLl4P3dH4L1VW47DNGYz4ZMF4eEyZZx8_40o6C2bnq9SrXqZUDsVQ7ov8mOqNY8Nw56IZnFZQBLvijElcYkRv?key=-AmqoHU_JCb21FYvySdS_g)

47.  Verify the setup by running `df -h`, output should look like below:

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXd7Ly8ZrpMaFmFcLHAoDWLB5yMjZVNb-dLq26qqGPP28QOd5DbLf4k0haMXKSQVpV-5YosNbjLXkR6XJjgPOLPHH44eD8UkSJge-uMcM2kzRI82o4cUackWsuGVh71RzL57FY-DaRv5BsyKb-3gi3_g8F7m?key=-AmqoHU_JCb21FYvySdS_g)

#### Step 3 - Install WordPress on your web Server EC2

1.  Update the repository

`sudo yum -y update`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXckcld7UiA1y42ztBBfe19nrGSe0ESpR_eG50OgvX40HR9tW3MFDiMhjdIRxvE6auLU5G9gefMwb3OnyC9TycomXv-cJd5Di1nJ2me7oexClA4gdpU7EVd7VWrpSZOu_PfoofG01QZyTdsv9VMRseIJLjXQ?key=-AmqoHU_JCb21FYvySdS_g)

2.  Install wget, Apache and it’s dependencies

`sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXe86hcD4cUfZutic3kBUicd8HigOFGec4jAI0t5Z3IPX4IoHO5x4P9g6Hm-76thquJ8jF-pXgddg5VtiySJo8wKh1fzeoI9T9ukT02U60boUWLLlUR5EU595gLO52KzZM5vfidAFOhzJklPfudsegx0NJzz?key=-AmqoHU_JCb21FYvySdS_g)

3.  Start Apache

`sudo systemctl enable httpd`

`sudo systemctl start httpd`

4.  To install PHP and it's dependencies

First, add the EPEL repository

`sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

Next, enable the Remi repository and install PHP:

`sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

`sudo yum module list php`

`sudo yum module reset php`

`sudo yum module enable php:remi-7.4`

`sudo yum install php php-opcache php-gd php-curl php-mysqlnd`

Start PHP-FPM:

`sudo systemctl start php-fpm`

`sudo systemctl enable php-fpm setsebool -P httpd\_execmem 1`

5.  Restart Apache

`sudo systemctl restart httpd`

6.  Download wordpress and copy wordpress to `/var/www/html` `mkdir wordpress` `cd wordpress`

    `sudo wget http://wordpress.org/latest.tar.gz sudo tar xzvf latest.tar.gz`

    `sudo rm -rf latest.tar.gz` 
    `cp wordpress/wp-config-sample.php wordpress/wp-config.php` 
    `cp -R wordpress /var/www/html/`

7.  Configure SELinux Policies

    `sudo chown -R apache:apache /var/www/html/wordpress`

    `sudo chcon -t httpd\_sys\_rw\_content\_t /var/www/html/wordpress -R`

    `sudo setsebool -P httpd\_can\_network\_connect=1`

#### Install mysql on Database server

`sudo yum update`

`sudo yum install mysql-server`

`sudo systemctl restart mysqld`

`sudo systemctl enable mysqld`

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXf97TTYpd_1Qj3syCbdLw-A_FDLtc5UVw6zshguY_5IYYF7PgL42z5xegVJFpt14-XraMtMF9u8VzONgaxYJyh5TtMoNbF-6M2paVImSyGwMYBvNIXrRUVOlNRLDALJciRxqwdYOLCq0A2bVnRb7DbWJFLT?key=-AmqoHU_JCb21FYvySdS_g)

##### configure DB to work with wordpress

`sudo mysql`

`CREATE DATABASE wordpress;`

`CREATE USER 'my\_wordpress'@'%' IDENTIFIED WITH mysql\_native\_password BY 'wordpress';`

`GRANT ALL PRIVILEGES ON \*.\* TO 'wordpress'@'%' WITH GRANT OPTION;`

`FLUSH PRIVILEGES;\`

##### See all users and hosts

`select user, host from mysql.user;`

#### Step 6 — Configure WordPress to connect to a remote database.

Hint: Do not forget to open MySQL port 3306 on DB Server EC2.

For extra security, we shall allow access to the DB server ONLY from your Web Server's IP address, so in the Inbound Rule configuration specify source as /32

Install MySQL client and test that you can connect from your Web Server to your DB server by using mysql-client

`sudo yum install mysql`

`sudo mysql -u admin -p -h <DB-Server-Private-IP-address>`

Verify if you can successfully execute `SHOW DATABASES;` command and see a list of existing databases.

Change permissions and configuration so Apache could use WordPress:

Enable TCP port 80 in Inbound Rules configuration for your Web Server EC2 (enable from everywhere 0.0.0.0/0 or from your workstation's IP)

Try to access from your browser the link to your WordPress http://<Web-Server-Public-IP-Address>/wordpress/

![](https://lh7-us.googleusercontent.com/docsz/AD_4nXegniJpyv7XB0l3-S2Mboym246drNKoMcrkHjV-0z4Dp2Rwsf4gEMApMHmuDi39SNuiWURmz-4M5m01f3kW1n4gWpKlNWyxHeMVY_mrZJzvRw_4S9CdW5EFbH3PTyR5bBLQJPGKZr23T68nwopPilnB7ys?key=-AmqoHU_JCb21FYvySdS_g)
