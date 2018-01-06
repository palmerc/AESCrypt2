## AESCrypt2

This is the original source code upon which the [Huawei HG8245 configuration encrypt/decrypt tool][1] was built. This router is used with Fiber customers in Oslo, Norway that are using [Get][3] as their ISP. Being able to encrypt and decrypt the firmware allows you to add a new user with super-user privileges or change the root/admin account to have the same access as Get provides themselves. The details are described in the first link. In summary, passwords are hashed using
`SHA256(MD5(admin))` which in this example yields  `465c194afb65670f38322df087f0a9bb225cc257e43eb4ac5a0c98ef5b3173ac`. You'll find this user in the config from Get and it has been given reduced privileges (level 1).

### Get user

As defined in the configuration file Get added a user called 'getaccess' and with level 0 privileges (the highest) 

    <X_HW_WebUserInfoInstance InstanceID="2" UserName="getaccess" Password="fc0fe4711c0263f37013e423fde0a8be0d64d45f231c924952327052db50b66f" UserLevel="0" Enable="1" ModifyPasswordFlag="1" PassMode="2"/>

The tarball can be download from [packetstormsecurity.com][2].

Based upon the analysis of the program:
   
   Huawei's encryption key is `hex:13395537D2730554A176799F6D56A239`

To recreate the functionality of the `aescrypt2_huawei` app you need to do the following:

   1) `echo -n 'hex:13395537D2730554A176799F6D56A239' > key.txt`
   2) `dd if=config.encrypted of=config_no_header.encrypted bs=1 skip=8`
   3) `./aescrypt2 1 config_no_header.encrypted config.decrypted.gz key.txt`
   4) `gunzip config.decrypted.gz`

After getting the encryption key and searching for it I found a spanish speaking forum that says they got the encryption key from a file found on the device in `/etc/wap/aes_string`.

[1]: https://zedt.eu/tech/hardware/obtaining-administrator-access-huawei-hg8247h/
[2]: https://packetstormsecurity.com/files/35655/aescrypt2-1.0.tgz.html
[3]: https://www.get.no
