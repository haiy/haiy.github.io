---
titile: tricks
layout: post
---

[edit tricks](https://github.com/haiy/haiy.github.io/edit/master/tricks.md)

[self](https://haihome.top/tricks)

========================

```
du -ms .[^.]* * | sort -nr
```

=======================

打开终端，查看：输入 diskutil list
找到对应的磁盘名称，加载：sudo diskutil mount /dev/disk2s3
输入密码
加载完成

=======================

关于乱码，中文编码https://en.wikipedia.org/wiki/Chinese_character_encoding
ISO-2022-CN CNS 11643 Big5 HKSCS GB 18030 GBK GB 2312 GB/T 12345 HZ ISO-IR-165 CCCII

vim尝试解决方法：
:e ++enc=gbk
:e ++enc=gb2312
:e ++enc=gb10830

简单来说都试着打开下。编码正常了，然后
:set fileencoding=utf-8
:wa!


=======================

python time format

import time    
time.strftime('%Y-%m-%d %H:%M:%S')
=======================

Connect Raspi to a Proxy

vim /etc/environment

export http_proxy="http://username:password@host:port/"

<https://www.raspberrypi.org/forums/viewtopic.php?t=18634>

apt proxy 

sudo vim  /etc/apt/apt.conf.d/95proxies

Acquire::http::Proxy "http://yourproxyaddress:proxyport";

====================================

bash redirect log

```bash
LOG_FILE=/tmp/both.log
exec > >(tee -a ${LOG_FILE} )
exec 2> >(tee -a ${LOG_FILE} >&2)
echo "this is stdout"
chmmm 77 /makeError
```

```bash
git ls-files --stage projectfolder
git rm —cached projectfolder

add submodule
git submodule add git@mygithost:billboard lib/billboard
```

To remove a submodule you need to:
1. Delete the relevant section from the .gitmodules file.
2. Stage the .gitmodules changes git add .gitmodules
3. Delete the relevant section from .git/config.
4. Run git rm --cached path_to_submodule (no trailing slash).
5. Run rm -rf .git/modules/path_to_submodule
6. Commit git commit -m "Removed submodule <name>"
7. Delete the now untracked submodule files rm -rf path_to_submodule

- https://stackoverflow.com/questions/12898278/issue-with-adding-common-code-as-git-submodule-already-exists-in-the-index
- https://chrisjean.com/git-submodules-adding-using-removing-and-updating/
- https://stackoverflow.com/questions/11258737/restore-git-submodules-from-gitmodules




```bash

====================================
查看cpu数
cat /proc/cpuinfo | grep processor | wc -l
nproc
lscpu
查看mem
free -m
/proc/meminfo 

====================================
ssh -ND port username@host

================================         
my_command || { echo 'my_command failed' ; exit 1; }

cmd1 && cmd2
will run cmd2 when cmd1 succeeds(exit value 0). Where as

cmd1 || cmd2
will run cmd2 when cmd1 fails(exit value non-zero).
Using ( ) makes the command inside them run in a sub-shell and calling a exit from there causes you to exit the sub-shell and not your original shell, hence execution continues in your original shell.

To overcome this use { }
The last two changes are required by bash.
https://stackoverflow.com/questions/3822621/how-to-exit-if-a-command-failed

================================         
* mount -t deviceFileFormat -o umask=filePermissons,gid=ownerGroupID,uid=ownerID /device /mountpoint
* mount -t vboxsf -o umask=0022,gid=33,uid=33 dev /var/www

https://superuser.com/questions/320415/linux-mount-device-with-specific-user-rights

================================         

wget mirror a website

```bash
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://example.org
wget -mkEpnp http://example.org
```

================================     

```
Pagination in Jekyll only works in an index.html file. If you have other pages in the root of your project folder (say, about.html, poems.html) pagination will NOT work in them.
To have pagination work in another page other than your index.html, create a new folder for that page (say, poems/) and change what would have been "poems.html" to "poems/index.html". After that, your "paginate_path" in _config.yml should be 'paginate_path: "poems/page:num/"'.
I'm still investigating this issue. My site needs pagination on multiple pages...something which Jekyll doesn't seem to support out-of-the-box
```

https://stackoverflow.com/questions/20829006/jekyll-paginator-not-working

================================        
# sum file lines

```bash
find . -type f  -exec cat {} + | wc -l
```

ref: https://stackoverflow.com/questions/13727917/use-wc-on-all-subdirectories-to-count-the-sum-of-lines

================================        
# mvn create a clean project 

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
```

[ref](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)



================================        
#  git 

 ## remove big files         

 git filter-branch --tree-filter 'rm -rf path/to/your/file' HEAD         
 ref: <https://stackoverflow.com/questions/8083282/how-do-i-remove-a-big-file-wrongly-committed-in-git>
 
 ## git-fetch-remote-branch
 git checkout --track origin/daves_branch
 
 <https://stackoverflow.com/questions/9537392/git-fetch-remote-branch>
 


================================       
# SimpleCGIServer:        
Procedure:       
    1.mkdir cgi-bin       
    2.mv ***.cgi cgi-bin/       
    3.python -m CGIHTTPServer 8000       
    4.http://xxxx:8000/cgi-bin/***.cgi       
Url:http://stackoverflow.com/questions/10396330/how-to-host-python-cgi-script-with-python-m-simplehttpserver-8000-or-python       
       
================================       
# SimpleSubnetMasks       
Url:http://www.subnet-calculator.com/cidr.php       
       
================================       
# Squid ProxyServer ShareHttpConnection       
1.find a stable versions on http://www.squid-cache.org/Versions/       
2.src code       
3.tar xzf squid*.*        
4.cd squid*        
5../configure       
6.make       
7.sudo make install       
8. whereis squid       
9.find the corresponding squid.conf       
10.change /usr/local/squid/etc/squid.conf       
    1)set the netmask to right value of localnet       
    e.g acl change "localnet src 10.0.0.0/8" to acl "localnet src 10.0.0.0/24" to        
    control the ip range       
    2) set the http_port       
        http_port 192.168.1.1:32780       
       
11.uncomment the cache_dir line       
12.       
/usr/local/squid/sbin/squid -z        
/usr/local/squid/sbin/squid        
13.check logs in /usr/local/squid/var/logs       
Url:http://wiki.squid-cache.org/SquidFaq/ConfiguringSquid       
       
================================       
# Use Proxy on Linux       
export http_proxy=http://<proxy host or IP>:<proxy port >        
export ftp_proxy=http://<proxy host or IP>:<proxy port >       
       
================================       
# Apache virtual host settings       
       
1.when permission denied errors occured, there may be two reasons,       
    1)permission of certain parent directory is not rwxr_xr_x.       
    2)the path is simply wrong!       
    3)forget to set the directory permissions in the conf       
    Here is an success example:       
       
       
    Listen 127.0.0.1:9080       
    NameVirtualHost *:9080       
    <Directory "/Users/haiy/hadoop">       
          Options +Indexes +ExecCGI +FollowSymLinks        
          DirectoryIndex index.cgi index.php index.html        
          AllowOverride Limit FileInfo Indexes Options        
          Order allow,deny        
          Allow from all        
    </Directory>       
    <VirtualHost 127.0.0.1:9080>       
        ServerName 127.0.0.1:9080       
        ErrorLog "/private/var/log/apache2/localhost_log"       
        CustomLog "/private/var/log/apache2/localhostlog" common       
        DocumentRoot "/Users/haiy/hadoop"       
    </VirtualHost>       
       
2.cgi dir settings Example       
    1)make sure the dir is reachable       
    2)alias the script dir       
    3)with correct script       
       
    Here is an success example:       
       
    <Directory "/Users/test_cgi">       
          AddHandler cgi-script .cgi .pl        
          Options +Indexes +ExecCGI +FollowSymLinks        
          DirectoryIndex index.cgi index.php index.html        
          AllowOverride Limit FileInfo Indexes Options        
          Order allow,deny        
          Allow from all        
    </Directory>       
    <VirtualHost 127.0.0.1:9080>       
        ServerName 127.0.0.1:9080       
        ErrorLog "/private/var/log/apache2/localhost_log"       
        CustomLog "/private/var/log/apache2/localhostlog" common       
        ScriptAlias "/cgi/" "/Users/test_cgi/"       
        DocumentRoot "/Users/haiy/Documents/test_project"       
    </VirtualHost>       
       
    How to access the cgi:       
    1)suppose there is file named hello.cgi       
    2)content of hello.cgi is :       
           
     #!/usr/bin/env python       
     print  "Content-Type: text/html"       
     print ""       
     print "Halo, I'm the first cgi!"       
       
     then, hello.cgi can be accessed from the url :       
     http://localhost:9080/cgi/hello.cgi       
       
================================       
# Linux HostName config       
1.check current hostname       
hostname       
2.set current hostname to my_pc immediately       
sudo hostname  my_pc       
3.make it effect permanent       
add my_pc to /etc/hostname  and remove others       
       
Url : http://askubuntu.com/questions/59458/error-message-when-i-run-sudo-unable-to-resolve-host-none       
       
================================       
# Ubuntu apt-get proxy setting       
sudo vim /etc/apt/apt.conf.d/01proxy       
The following text was added:       
$Acquire::http::Proxy "http://mywindowsdomain\fossfreedom:password@askubuntu-proxy.com:8080"       
If you are using an anonymous proxy then you don't need your login credentials:       
$Acquire::http::Proxy "http://askubuntu-proxy.com:8080";       
       
================================       
# How to get a single clean file from github       
1.just change to the file page       
2.click the view style as raw       
3.and then it can also be downloaded directly       
       
================================

```

Mirror <a href="/mirrors.html">mirror list</a>       
