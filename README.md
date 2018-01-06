## AESCrypt2

This is the original source code upon which the [Huawei HG8245 configuration encrypt/decrypt tool][1] was built.

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
