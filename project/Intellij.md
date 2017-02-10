# IntelliJ IDE Configuration 


## Preparations
Once you `File` > `New` > `Project From Existing Sources`, IntelliJ will automatically detect your existing configurations, such as:
- Auto detect Maven Project
- Your Spring and Hibernate Framework

It will show as `Event Log` just bottom right of your window as green icon and fade-in notifications.

Follow the instructions to complete the initialization.

### Install Plugins
In the following instructions you could probably encounter a problem that you cannot find the corresponding plugin or tools for it, so please walk through the following: 
1. Open `File` > `Settins` > `Plugins`
2. Search the key word. If no result, press `Install JetBrains Plugin` Below the list.
3. Find what you want and click `Install`.

## Tomcat Configuration
We need to setup a tomcat server first in `Settings`. 
To open `Settings`, you can find it in menu `files` > `Settings`, or use hotkey `Ctrl+Alt+S`.

### Server Setup
1. Open `Settings`.
2. Go to `Build, Execution, Development`, find `Application Servers`.
3. Press green `+`, pick `Tomcat Server`, then config it
```
Example:
Tomcat Home:D:\apache-tomcat-8.0.35
Tomcat base directory: D:\apache-tomcat-8.0.35
```

### Config Server for Project

1. Find `▼` on top right of you window, then `Edit Configuration...`.
2. In `Run/Debug Configurations` window, click green '+', Select `Tomcat Server` > `Local`
3. In `Server` tab, default setting is far enough for uses.
4. But the cat icon still being attached a red cross. Go to `Deployment` tab and select an Aritifact to deploy. Usually use `exploded` one.	
5. Fill your project name into `Application Context`.
5. Save and close.

### Config One Server for Multiple Project
Some of our projects need to be ran under unique server & port, so we need to setup an remote server.

1. Follow the steps in previous instruction `Config Server for Project` to setup tomcat for Project A.
2. Open Project B, open `Run/Debug Configurations`, after clicking the green `+`, choose `Tomcat` and `Remote`.
3. Keep same port JMX Port, Port num and set Host to "localhost" by default.
4. In `Deployment` tab, it's the same as previous, `Application Context` should be varied between projects.
5. Save and close.

## Perforce 4V Configuration

### VCS Setup
We need to setup version controls before start applying it to projects.
1. `Settings` > `Version Control` > `Perforce`. You can refer to the images below. `Client` is your perforce workspace name, displaying in your perforce window's title.
![vsc1_img](https://github.com/helisz/dict/blob/master/_asserts/images/vcs1.jpg)

2. Save and close.
### Perforce Intergration
1. Go to menu `VCS` > `Enable Version Control Intergration`, select `Perforce` in dropdown menu, then press `ok`.
2. Now you can use VCS down/up icon on right top of window,.

## SCSS Configuration
`File Watcher` is the tool that can be configured to watch the change on your file and compile to what you want. You have to make sure that you already installed it ahead of time.

Here I use SCSS for example.
1. Please make sure you have already installed Ruby and Ruby-sass.
`$ sudo apt-get install ruby-full`
`$ sudo gem install sass"`
Suppose your Ruby's directory is `C:\Ruby23-x64`
2. Go to `Settings` > `Tools' > `File Watchers`.
3. Click green `+`, then config it.
```
[Example]
File Type:		SCSS
Scope:			Project File
Program: 		C:\Ruby23-x64\bin\scss.bat
Arguments:		--no-cache --update $ProjectFileDir$\WebContent\resources\scss:$ProjectFileDir$\WebContent\resources\css
Working Dir.:  	$ProjectFileDir$\WebContent\resources\scss
Env. Var.: 		[BLANK]
Output Path.: 	$FileNameWithoutExtension$.css:$FileNameWithoutExtension$.css.map
```

Possible issue: `...Errno::EACCES: Permission denied @ rb_sysopen - ...`
Solution: Go to perforce, and checkout related .css file.
