After opening `pcap` file in wireshark we got some HTTP trafic

![image](https://user-images.githubusercontent.com/44019881/161449828-92d47df9-0bd1-486c-9be0-b968f16513bf.png)

But every post is differetn by last letter in url. After saving this output to a file. Last letters of every post can be extracted

```bash
grep POST exported_http | grep -v browse | awk -F_ '{print $2}'| awk '{print $1}' | sed -z 's/\n//g;s/+/ /g;s/%7B/{/g;s/%7D/}/g
```

```
Treasure PlanetDuneVoltron in SpaceTreasure PlanetDuneHighlanderHighlanderVoltron in SpaceDuneStar Trekshctf{T1m3-is-th3-ultimat3-curr3Ncy}Star Warsshctf{T1m3-is-th3-ultimat3-curr3Ncy}shctf{T1m3-is-th3-ultimat3-curr3Ncy}Star TrekDuneshctf{T1m3-is-th3-ultimat3-curr3Ncy}Battlestar GalaticaStar WarsStar TrekBattlestar Galaticashctf{T1m3-is-th3-ultimat3-curr3Ncy}Battlestar GalaticaDuneDuneVoltron in SpaceHighlanderTreasure PlanetHighlanderStar TrekStar TrekTreasure Planetshctf{T1m3-is-th3-ultimat3-curr3Ncy}Star WarsBattlestar GalaticaStar TrekBattlestar GalaticaTreasure Planetshctf{T1m3-is-th3-ultimat3-curr3Ncy}Voltron in SpaceVoltron in SpaceVoltron in Space
```

`shctf{T1m3-is-th3-ultimat3-curr3Ncy}`
