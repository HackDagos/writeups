# **Writeup - VishwaCTF**

* Category **Forensics**
* Name **Mistery Of Oakville Town**
* Difficulty **Medium**

## Description
> On March 27, 2023, a golden sceptre was taken from Oakville Town Hall. Suspect Johannes Trithemius has been taken into custody by Detective Jameson. Jameson believes he is the town's fugitive thief's right-hand man. Jameson was able to retrieve one image that he thinks contains details about the vehicle the thief fled in, even though Johannes had erased all digital traces from the device. There are four intertown highways in Oakville, and they are constantly closely watched. The database contains all the data on the roads as well as the data on the residents of the towns. Find the thief and town name he escaped to. Watch out for Johannes, a cunning con artist who frequently knows how to trick the police.
> Flagformat: VishwaCTF{FirstNameLastNameTown}

We are given two files, a jpeg image and a sqlite3 database.

## **Solution**
Initially, we tried to search the db for the license plate showed in the image, without success.
After that, based on the timestamp of the image (27/03/2023 21:45) we can query the db to see if there's any car that had been seen at that time.
```
sqlite> select * from traffic_cam3 where year='2023' and month='3' and day='27' and hour='21';
id|towards_town_code|year|month|day|hour|minute|license_plate
715|SW|2023|3|27|21|45|OV-007
```

Ok, now we can search the name:
```
sqlite> select name from people where license_plate='OV-007';
name
Wellington East
```

And the town name:
```
sqlite> select town_name from town_code where town_code='SW';
town_name
Springwood
```

`VishwaCTF{WellingtonEastSpringwood}`
