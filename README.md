# Aria2TrayIcon
Aria2TrayIcon as the repo name explains is a tool designed to add an tray icon on desktop platforms for easily running the aria2 deamon but it also does more!
Push requests are welcome.

#### Feature list:
* Commands to shutdown the aria2 deamon using the jsonrpc
* Integrated web server for serving the web ui
* If enabled it opens the system default web browser on startup
* Portable

#### Latest Version: 1.0.0

#### Building
1. Clone the repo ```git clone https://github.com/luckcolors/Aria2TrayIcon.git```
2. Resolve the dependencies: ```go get github.com/luckcolors```
3. ```cd Aria2TrayIcon```
4.  * Windows: Build with the command ```go build -ldflags -H=windowsgui Aria2TrayIcon``` this disables the console window from appearing.
      *OS X and Linux: as simple ```go build Aria2TrayIcon``` should do.

#### Configuration

In the same directory where you want to keep the Aria2TrayIcon executable download the config sample file and rename it to ``` aria2TrayIconConf.json ```.
Change the values to better fit your setup.
Here are some info:
Note: If you end up using a path or special characters be sure to follow json's character escape sequence. http://json.org/
```
{
  "command": "./aria2c.exe",
    Aria2 executable name, it can also be a path to it
    
  "args": "--conf-path=aria2.conf",
  This are the arguments to pass to aria2 usually you only want to pass the --config-path= 
    
  "iconFile": "icon.ico",
 Path to the icon file to use must be .ico on windows.(the icon files can be found in the repo. Those are from the original aria2 website's favicon.). 
  
  "aria2Token": "TOKEN",
  Aria2 json rpc token this is mandatory in order for the systray buttons work.
  
  "aria2RpcUrl": "http://localhost:PORT/jsonrpc", 
   url to the json rpc.
   
  "runHttpServer": true, 
  Wheter to run the webui webserver or not.
  
  "httpDataFolder": "webui", 
  Path to the webui folder.
  
  "httpServerHost": "INTERFACE:PORT",
  Host setting for the webserver, the interface can be omitted. Example: ":1234".
  
  "osOpenHttp": true,
  Wheter to open the url with a browser or not.
  
  "osOpenHttpUrl": "http://localhost:PORT",
  This should be the same host and port used by the serverHost setting with http:// added at the beginning.
  
  "osOpenHttpUrlCommand": "cmd", 
  The command to use for opening the url this changes based on the os you are running: 
  MacOSX:
  "osOpenHttpUrlCommand": "open",
  "osOpenHttpUrlCommandArgs": "",
  Linux: it varies on the distribution you're using.
  
  "osOpenHttpUrlCommandArgs": "/c start" 
  Arguments for the command.
}
```
After you have configured the systray it's important to configure Aria2 with the required settings:
Note: if you don't want to use the config file you can simply put those lines in the argument of the aria2 command for example:  ```enable-rpc=true ``` becomes ```--enable-rpc=true```. 
Note: For more info you can checkout the Aria2 official documentation [here](https://aria2.github.io/manual/en/html/aria2c.html#options) 

```
enable-rpc=true
This enables the json rpc.

rpc-secret=TOKEN
This is the key used for authenticating on the json rpc.
This shoudl be the same as "aria2Token".

rpc-listen-all=false
This makes it so it only listens locally on your pc.

rpc-listen-port=PORT
Port for the json rpc to listen on. This should be the same as "aria2RpcUrl"
```
#### Libraries used
 
- [getlanter/systray](https://github.com/getlantern/systray)
It's the base of this program. Currntly i'm using my own fork [here](https://github.com/luckcolors/systray) as i'm wainting for the pactch i made to be merged.
- [paked/configure](https://github.com/paked/configure) 
Library for pasing json configuration files.
- [labstack/echo](https://github.com/labstack/echo)
-[labstack/echo/engine/fasthttp](https://github.com/labstack/echo/engine/fasthttp)
Web frameworks used for the web ui server.

####Credits
Me [luckcolors](https://github.com/luckcolors) 
And [Stefanoz45](https://github.com/Stefanoz45)
for general advice and help.

####License: MIT
