# **Writeup - HackPackCTF**

* Category **WEB** 
* Name **WolfHowl** 
* Difficulty **Easy**


## Description

> Log into WolfHowl website
>[wolfhowl.cha.hackpack.club](https://wolfhowl.cha.hackpack.club)

## **Solution**

The site presents itself to us like this:

![site](img/WolfHowl_site.png)

if we try to register we will be told that registration is disabled, so we can discard a 
possible attack on /register or /login

![error registration](img/WolfHowl_disabled.png)

at this point we are left to check only the search field, if we go to type `"'"` in the search bar the system will respond with an error

![error PDO](img/WolfHowl_error.png)

excellent, we discovered a possible field where to perform a SQL injection! 
at this point, we do a basic injection and see what happens:


`"OR 1=1 --"`

ok by forcing the field to True the site responds to us with all the artists in the database at this point we have confirmation of a SQL injection

![list all artists](img/WolfHowl_or.png)

we can start the database enum
the first thing we need to do is to figure out how many rows the main select returns, to do this we need to run the following query: 

`"UNION SELECT @@VERSION --"`

we get an error returned on the number of rows, this is because the two select (the source one and ours) do not return the same number of rows, we add fields until we catch the same number of rows

![error select rows](img/WolfHowl_select_error.png)

`"UNION SELECT @@VERSION,2,3,4 --"`

![select enum rows](img/WolfHowl_select_enum_rows.png)

perfect! now we can start gathering information about where the flag is stored, let's start by listing the database columns:

`"UNION SELECT table_schema, table_name, column_name,4 FROM information_schema.columns -- "`

![list tables](img/WolfHowl_list_tables.png)

uh! in the employee table we have the columns email and password

![list tables](img/WolfHowl_list_tables2.png)

Now we have all the necessary information; let's list the users

`"UNION SELECT email,password,Title,4 FROM employee -- "`

![list users](img/WolfHowl_users.png)

perfect we have the credentials! 
let's try logging in as GM

![flag](img/WolfHowl_flag.png)

flag : ***flag{art_decorates_space_but_music_decorates_time}***
