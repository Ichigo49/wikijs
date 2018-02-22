<!-- TITLE: Install -->
<!-- SUBTITLE: Les installs & Conf particulières -->

# WIKI.JS
Parceque c'est tout frais !
*  [Node.js](https://nodejs.org/en/download/package-manager/)
*  MongoDB
*  Git :

```sh
echo "deb http://ftp.us.debian.org/debian testing main contrib non-free" >> /etc/apt/sources.list \
         &&      apt-get update              \
         &&      apt-get install -y git      \
         &&      apt-get clean all
```

