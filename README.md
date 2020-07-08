<p align="center">
  <img width="480" height="480" src="https://media.giphy.com/media/IzQYP4hkIrgxnoVPBR/giphy.gif">
</p>
<p align="center"><img src="https://img.shields.io/badge/Version-1.0-brightgreen"></p>

</p> 
<p align="center"><img src="https://img.shields.io/badge/Author-Yezz123-green.svg"> 
</p>


<p align="center">
  <a href="https://github.com/yezz123">
    <img src="https://img.shields.io/github/followers/yezz123?label=Follow&style=social">
  </a>
  <a href="https://github.com/yezz123/unfollo/stargazers">
    <img src="https://img.shields.io/github/stars/yezz123/CryptoPass?style=social">
  </a>
</p>
<p align="center">
 Get unencrypted 'Saved Password' from Google Chrome.
</p>

## Introduction
Like other browsers Chrome also has built-in login password manager functionality which keeps track of the login secrets of all visited websites. Whenever user logins to any website, he/she will be prompted to save the credentials for later use and if user chooses so, then the username & passwords will be stored in internal login database. So next time onwards whenever user visits that website, he/she will be automatically logged in using these stored credentials which saves hassle of entering the credentials every time.

Chrome stores all the sign-on secrets into the internal database file called 'Web data' in the current user profile folder. Newer version has moved the login passwords related database into new file named 'Login Data'.This database file is in SQLite format and contains number of tables storing different kind of data such as auto complete, search keyword, ie7logins etc in addition to login secrets.

The logins table mainly contains the information about sign-on secrets such as website URL, username, password fields etc. All this information is stored in the clear text except passwords which are in encrypted format. 

#### Mac/Linux Implementation
Encryption Scheme: AES-128 CBC with a constant salt and constant iterations. The decryption key is a PBKDF2 key generated with the following:

* salt is b'saltysalt'
* key length is 16
* iv is 16 bytes of space b' ' * 16
* on Mac OSX:
  * password is in keychain under Chrome Safe Storage
    * I use the excellent keyring package to get the password
    * You could also use bash: security find-generic-password -w -s "Chrome Safe Storage"
  * number of iterations is 1003
* on Linux:
  * password is peanuts
  * number of iterations is 1
  
#### Windows Implementation
Google Chrome encrypt the password with the help of CryptProtectData function, built into Windows. Now while this can be a very secure function using a triple-DES algorithm and creating user-specific keys to encrypt the data, it can still be decrypted as long as you are logged into the same account as the user who encrypted it.The CryptProtectData function has a twin, who does the opposite to it; CryptUnprotectData, which... well you guessed it, decrypts the data. And obviously this is going to be very useful in trying to decrypt the stored passwords.

## Python Implementation (Working)

#### Usage
```python
>>> from chrome_passwd import ChromePasswd
>>> chrome_pwd = ChromePasswd()
>>> print(chrome_pwd.get_login_db)
/Users/x899/Library/Application Support/Google/Chrome/Default/
>>> chrome_pwd.get_password(prettyprint=True)
{
	"data": [
		{
			"url": "https://github.com/",
			"username": "FR1234",
			"password": "secretP@$$w0rD"
		},
		{
			"url": "https://accounts.google.com/",
			"username": "Simo233@gmail.com",
			"password": "@n04h3RP@$$m0rC1"
		}
	]
}
```

<p align="center">
  Follow Me On
</p>
<p align="center">
  <a href="https://www.youtube.com/channel/UC5ba_E8pgMV0ETCRn7PQzUg?view_as=subscriber">
    <img src="https://www.iconsdb.com/icons/preview/black/youtube-4-xxl.png" width="40" height="40">
  </a>
  <a href="https://instagram.com/froggy__19">
    <img src="http://clipart-library.com/images_k/instagram-png-transparent/instagram-png-transparent-16.png" width="40" height="40">
    </a>
</p>
