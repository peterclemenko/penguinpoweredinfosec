Steam Browser Forensics
=======

Overview
---------
The Steam digital distribution platform is the most popular digital distribution client in the world for PC gaming. It includes three main components with web browser integration, the client, Big Picture, and the in-game overlay.

The Steam browser components are based on Webkit.  The browsers were originally based on Trident, howeveri it was changed to Webkit shortly before Steam was released on Mac OSX.

Note: This article only covers artifacts left behind by the Webkit version. if you have documentation on the Trident version, or artifacts of the Trident version that I can analyze, please drop me a line on the issue tracker for the wiki.

Common Artifacts
---------
All of the steam components that use a browser store cookies, cache, and local storage files. Local storage files and cookies are in the form of an SQLite 3 database that can be opened with a database browser.

Note: The Cookies and localconfig files are stored in SQlite 3 databases. 

Note: The cache stores raw files without extensions in a file name schema similar to f_0001a

While you have to manually add an extension in Windows, Linux will automatically detect the MIME type of the file and even show a preview in the file explorer. Autopsy can usually automatically detect the MIME types of these files as well.


Cookies table database structure

![](dfir/browserforensics/steam/cookiesdbstructure.png "Cookies table database structure")


Cookies table example entry

![](dfir/browserforensics/steam/cookiestableexample.png "Cookies table example entry")


Local storage example entry

![](dfir/browserforensics/steam/localstorageignexampleentry.png "Local storage example entry")


Local storage schema

![](dfir/browserforensics/steam/localstorageschema.png "Local storage schema")

Client
---------

The client stores web history and data on what has been browsed to in the Steam client itself. This includes the store, community pages, workshop, and anything opened in a browser by the Steam client. The client only stores cookies, localconfig files, and a cache.

Note: The "Cookies" file is located at: ```/steam/config/htmlcache/Cookies```

Note: The raw cache files are located at: ```/steam/config/htmlcache/(file name here)```

A screenshot of the Steam forums in the client:

![](dfir/browserforensics/steam/steamclient.png "Steam client")

Big Picture
---------


A screenshot of Steam Big Picture mode's browser:

![](dfir/browserforensics/steam/steambigpicture.png "Steam Big Picture mode")

Note: Big picture history and favorites are stored in the sharedconfig.vdf file at the location:
```[Steam install directory]\userdata\<account id>\7\remote\sharedconfig.vdf```

Note: VDF files are text based configuration files that you can open in Notepad or your favorite text editor. In the vdf file, you will find a section called "Web" which stores the Steam Big Picture favorites and history.

Note: Steam refers to the Big picture mode as "Tenfoot".

Note: Big Picture mode only stores the six most recent and top six visited pages in it's history.

Note: The "Cookies" file is located at: ```/steam/config/htmlcache/Cookies```

Note: The raw cache files are located at: ```/steam/config/htmlcache/(file name here)```

An example of the web history and favorites in Big Picture:

```
"Web"
	{
		"WebFav0_URL"		"https://www.google.com/"
		"WebFav0_Name"		"Google"
		"WebFav1_URL"		"http://www.youtube.com/"
		"WebFav1_Name"		"YouTube"
		"WebFav2_URL"		"http://www.twitter.com/"
		"WebFav2_Name"		"Twitter"
		"WebFav3_URL"		"http://www.facebook.com/"
		"WebFav3_Name"		"Facebook"
		"WebFav4_URL"		"http://www.reddit.com/"
		"WebFav4_Name"		"Reddit"
		"WebRecent0_URL"		"http://www.linux.com/"
		"WebRecent0_Name"		"Linux.com | The source for Linux information"
		"WebFrequent0_URL"		"https://bitbucket.org/"
		"WebFrequent0_Name"		"Free source code hosting for Git and Mercurial by Bitbucket"
		"WebFrequent0_Access"		"3"
		"WebRecent1_URL"		"http://www.youtube.com/"
		"WebRecent1_Name"		"YouTube"
		"WebFrequent1_URL"		"http://www.armaholic.com/"
		"WebFrequent1_Name"		"Armaholic - Covering the Arma series - Arma 3 | Arma 2: Operation Arrowhead | Arma 2 | Arma 2: British Armed Forces | Arma 2: Private Military Company | Armed Assault"
		"WebFrequent1_Access"		"3"
		"WebRecent2_URL"		"http://www.reddit.com/"
		"WebRecent2_Name"		"reddit: the front page of the internet"
		"WebFrequent2_URL"		"http://digg.com/"
		"WebFrequent2_Name"		"Digg - What the Internet is talking about right now"
		"WebFrequent2_Access"		"1"
		"WebRecent3_URL"		"https://www.google.com/"
		"WebRecent3_Name"		"Google"
		"WebFrequent3_URL"		"https://www.kernel.org/"
		"WebFrequent3_Name"		"The Linux Kernel Archives"
		"WebFrequent3_Access"		"1"
		"WebFav5_URL"		"https://github.com/"
		"WebFav5_Name"		"GitHub · Build software better, together."
		"WebRecent4_URL"		"http://www.fark.com/"
		"WebRecent4_Name"		"Drew Curtis' FARK.com"
		"WebFrequent4_URL"		"http://www.amazon.com/"
		"WebFrequent4_Name"		"Amazon.com: Online Shopping for Electronics, Apparel, Computers, Books, DVDs & more"
		"WebFrequent4_Access"		"1"
		"WebRecent5_URL"		"http://www.armaholic.com/"
		"WebRecent5_Name"		"Armaholic - Covering the Arma series - Arma 3 | Arma 2: Operation Arrowhead | Arma 2 | Arma 2: British Armed Forces | Arma 2: Private Military Company | Armed Assault"
		"WebFrequent5_URL"		"http://store.steampowered.com/"
		"WebFrequent5_Name"		"Welcome to Steam"
		"WebFrequent5_Access"		"1"
		"WebFav6_URL"		"http://www.linux.com/"
		"WebFav6_Name"		"Linux.com | The source for Linux information"
	}

```



Overlay
---------

The overlay stores web history and data on what has been browsed to in the Steam in-game overlay. The overlay only stores cookies, localconfig files, and a cache.


