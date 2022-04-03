Provided file is with useless extension `chr` and ouptut of file provide no additional help, but examinig the first couple of bytes provide with hint that could be `PNG` file.

![image](https://user-images.githubusercontent.com/44019881/161450014-f960ee4e-ddd5-47df-9ae3-ae1f8894748a.png)

First bytes look like scrambled `PNG` and `IHDR` the header and first chuck of the `PNG` file.

The proper bytes are

![image](https://user-images.githubusercontent.com/44019881/161450025-c33a817b-774f-46a6-8097-79d0449ae2ba.png)

[List of file signatures - Wikipedia](https://en.wikipedia.org/wiki/List_of_file_signatures)

After changing header in hexeditor 

![image](https://user-images.githubusercontent.com/44019881/161450043-8f58a9f7-46e2-4018-83d4-9105d36e0958.png)

`file` still do not recognize it as `PNG` but `pngcheck` does and provide with additional data

![image](https://user-images.githubusercontent.com/44019881/161450051-14bfed59-5f97-4224-9f3a-83a261484c90.png)

To repair that chunk we need to change the blue-makred bytes because 4 bytes before(marked red underline) is length of `IHDR` chunk

![image](https://user-images.githubusercontent.com/44019881/161450063-6acab631-3256-459e-b098-f0e96aa27496.png)

![image](https://user-images.githubusercontent.com/44019881/161450065-c00b2abc-38c1-4411-9889-79626f3b8d91.png)

After changing bytes to be `IHDR`

![image](https://user-images.githubusercontent.com/44019881/161450078-b40a8c6e-7d17-4b26-a8c5-dfdcb994da65.png)

`pngcheck` complains about `IHDR` legnth

![image](https://user-images.githubusercontent.com/44019881/161450082-d08aa66d-7ea1-4b7b-9215-ab528ad2450a.png)

`IHDR` chunk contains various information

```
   Width:              4 bytes
   Height:             4 bytes
   Bit depth:          1 byte
   Color type:         1 byte
   Compression method: 1 byte
   Filter method:      1 byte
   Interlace method:   1 byte
```

And all this adds to 13 bytes so `0xD` in hex so we set that value in the length of `IHDR` chunk

![image](https://user-images.githubusercontent.com/44019881/161450089-53bb2e90-e7f1-4fcb-9a0b-67be6ed6798b.png)

After that change there is no more errors, `file` recognize this file as `PNG` and `pngcheck` says there everything allright
![image](https://user-images.githubusercontent.com/44019881/161450103-881b40f6-906a-4915-b9a4-5103d9397e30.png)

And this is the flag
![image](https://user-images.githubusercontent.com/44019881/161450113-eb17ddec-3fee-4f87-abba-0ec880bcfdf4.png)
