## Github : Signing commits using GPG (Ubuntu/Mac) :closed_lock_with_key:

* Do you have an Github account ? If not create one.
* **Install required tools**
* Latest [Git Client](https://git-scm.com/downloads) 
* gpg tools 
```
# Ubuntu
sudo apt-get install gpa seahorse
# MacOS with https://brew.sh/
brew install gpg
```
* Generate a new gpg [key](https://help.github.com/articles/generating-a-new-gpg-key/)
```
gpg --gen-key
```
* Answer the questions asked
> Note: When asked to enter your email address, ensure that you enter the verified email address for your GitHub account.

* **List generated key**
```
gpg --list-secret-keys --keyid-format LONG
```
* Above command should return like this
```
/home/username/.gnupg/secring.gpg
-------------------------------
sec   4096R/<COPY_LONG_KEY> 2016-08-11 [expires: 2018-08-11]
uid                          User Name <user.name@email.com>
ssb   4096R/62E5B29EEA7145E 2016-08-11

```
* Note down your key ```COPY_LONG_KEY``` from above (without `<` and `>`)
* **Export this (public) key to a text file**
```
gpg --armor --export <PASTE_LONG_KEY_HERE> > gpg-key.txt
```
* Above command will create a new txt file ```gpg-key.txt```

* **Add this key to GitHub**
* Login to Github and goto profile [settings](https://github.com/settings/keys)
* Click ```New GPG Key``` and paste the contents of ```gpg-key.txt``` file then save

* **[Tell](https://help.github.com/articles/telling-git-about-your-gpg-key/) git client to auto sign your future commits**
* Use the long key from above in next command
```
git config --global user.signingkey <PASTE_LONG_KEY_HERE>
git config --global commit.gpgsign true
```
* You are done, next time when you commit changes; gpg will ask you the passphrase.

### Make gpg remember your passphrase (tricky)
To make it remember your password, you can use ```gpg-agent```

Edit your ```~/.gnupg/gpg-agent.conf``` file and paste these lines
```
default-cache-ttl 28800
max-cache-ttl 28800
```
*28800 seconds means 8 hours*

If gpg-agent is not running you can start it with this command
```
gpg-agent --daemon
```

### Change your key passphrase
```
gpg --edit-key <PASTE_YOUR_KEY_ID_HERE>
```
At the gpg prompt type:
```
passwd
```
Type in the current passphrase when prompted<br>
Type in the new passphrase twice when prompted<br>
Type:
```
save
```

### Reference links
* https://help.github.com/articles/signing-commits-with-gpg/
* http://nishanttotla.com/blog/signing-git-commits-gpg/
* https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work
* https://news.ycombinator.com/item?id=7792026
* https://overflow.no/blog/2016/08/11/signed-commits-with-gpg-git-and-github-on-linux/
* http://stackoverflow.com/questions/10161198/is-there-a-way-to-autosign-commits-in-git-with-a-gpg-key
* http://irtfweb.ifa.hawaii.edu/~lockhart/gpg/gpg-cs.html
* https://help.ubuntu.com/community/GnuPrivacyGuardHowto
* https://medium.com/@timmywil/sign-your-commits-on-github-with-gpg-566f07762a43#.aovevj80y
* https://blog.erincall.com/p/signing-your-git-commits-with-gpg
* https://dev.to/agrinman/spoof-a-commit-on-github-from-anyone-4gf4
