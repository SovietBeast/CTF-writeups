# Enumeration

In home directory of `leonardo` user there are two files:

- noteToAdministraotr.txt

![image](https://user-images.githubusercontent.com/44019881/158075361-ce9a077b-9c42-4c8c-ac8f-f7ae1d9dbb54.png)

- list.txt

![image](https://user-images.githubusercontent.com/44019881/158075369-989d091b-ff9c-4155-9607-f05da91e767a.png)

`OneRule` could be a hint to `OneRuleToRuleThemAll` hashcat rule. 

`Linpeas` output showed that `sudoers` file was readable, and user `leonardo` can run `diff` binary as root. 

![image](https://user-images.githubusercontent.com/44019881/158075378-80efad57-14e6-458f-aff2-4b21612457cb.png)

With that reading `/etc/shadow` is possible.

![image](https://user-images.githubusercontent.com/44019881/158075387-253d3a24-1550-4f50-bf95-cf19b2332d33.png)

To crack hashes custom wordlist was made that contained favouire songs and artists from `list.txt` file.

```
The Notorious B.I.G. - Juicy
The Notorious B.I.G
Juicy
Snoop Dogg - Who Am I
Snoop Dogg
Who Am I
Kanye West - Diamonds From Sierra Leone
Kanye West
Diamonds From Sierra Leone
Outkast - Southernplayalisticadillacmuzik 
Outkast
Southernplayalisticadillacmuzik 
Drake - War
Drake
War
Alpha Wann - ÇA VA ENSEMBLE
Alpha Wann
ÇA VA ENSEMBLE
Freeze Corleone 667 - Freeze Raël
Freeze Corleone 667
Freeze Raël
Alpha Wann - apdl
Alpha Wann
apdl
Lomepal - A ce soir
Lomepal
A ce soir
Paris c'est loin - Booba
Paris c'est loin
Booba
```

And as hinted in `noteToAdministrator.txt` this was ran against hashcat `OneRuleToRuleThemAll` rule.

```bash
hashcat --force leonardo_w -r OneRuleToRuleThemAll.rule --stdout >newword
```

With that custom wordlist `administrator` password was cracked.

`administrator:oLmepaloLm`

![image](https://user-images.githubusercontent.com/44019881/158075400-0f18f3ee-105c-424f-ad1e-740452de34ca.png)

This set of credential allowed to login as `administrator` user.
![image](https://user-images.githubusercontent.com/44019881/158075411-4fa45cd1-b619-4e43-8836-a9e1c4b7ab4b.png)
