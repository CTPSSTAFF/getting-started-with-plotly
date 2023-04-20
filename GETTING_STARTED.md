# Getting Started with Plotly
This repository is devoted to getting you started creating data visualizations with the plotly.js library.
It describes what you'll need to work with plotly, offers instructions on creating your first visualization
with plotly (and tweaking it!), and provides "templates" for the most common types of visualizations 
that you can copy and modify.

Have fun!

## What's required
First things first: you need to have a few things lined up in order to get started.
You will need the following:
* Anaconda (including Python)
* A web browser (Google Chrome preferred)
* A text editor, such as Notepad++, VS Code, Sublime Txt, Emacs, or Vim
* A place to store files

### Anaconda (including Python)
Anaconda should be installed on all CTPS laptops. Check the Start menu, and make sure that
there's an entry for __Anaconda \(64-bit\)__, and that under it, there's an entry for 
__Anaconda Prompt \(anaconda 3\)__.
If you can't find these on your laptop, inform CPTS's Computer Resources group and ask
to have Anaconda installed on your system.

### A web browser
Similarly, the Chrome web browser should be installed on all CTPS laptops.
If it's not installed on your laptop, inform CPTS's Computer Resources group and ask
to have it installed.

### A text editor
In order to create data visualization with plotly, ou'll need a way to edit (create and modify) __text__ files.
Such a tool is called a __text editor__.
Text files _can_ be edited with Window's built-in _Notepad_ utility. But because _Notepad_ has _very_ limited functionality,
using it to do anything beyond the most elementary editing quickly becomes frustrating.
There are a number of alternatives, at least some of which are very easy to learn.

[Notepad++](https://notepad-plus-plus.org/) is recommnded for most users. 
It has all the functionality (and more) required to create data visualizations with plotly, and is very easy to learn. 
You can install Notepad++ on your CTPS laptop if you have 'Admin' priveledges
on it; if not, ask the CTPS Computer Resources staff to install it for you.

Microsoft [VS Code](https://code.visualstudio.com/) or [Sublime Text](https://www.sublimetext.com/) 
are recommended for people whose work involves writing a lot of code in general \(not just data visualizations\).

Finally, die-hard nerds might consider [GNU Emacs](https://www.gnu.org/software/emacs/) or [Vim](https://www.vim.org/download.php).
Emacs is the preferred editor of the suspecies of nerd found in the MIT habitat; Vim is preferred by the subspieces found in the Bell Labs habitat.

__Note:__ Microsoft _Word_ is __not__ a _text eitor_; it is a _word processor_. __Do not use MS Word to create data visualizations!__
Text editors work with text __as-is__, whereas word processors add all kinds of fancy-dancy formatting "stuff" to the raw text you enter. 
This formatting "stuff" gets written to disk along with the raw text you've entered, and will confuse the software \(the plotly library
and the plotly instructions you enter\) when plotly tries to generate a data visualization. \(For those who are curious, a useful
exercise is opening an MS Word document with Notepad++ and inspecting the contents. It doesn't look much like the text you enetered!\)

### A place to store files
Find (or create) a folder on your laptop or your favorite file server in which to store the files you create 
when developing plotly. __Please note: A folder in Google Drive is not suitable for this purpose.__

## Plotly visualization 101
This section will walk you through creating your first visualization with plotly - a pie chart that 
displays the transportation "mode share" for the City of Boston from 1990 to 2014. 
The data was taken from a document on the City of Boston's website (
The structure of the code have been unashamedly borrowed from plotly's own website, 
but I've added quite a bit of background information that's not given there.

These are the steps we will be going through:
1. Identifying a place in which to work
2. Creating a web server
3. Creating your first visualization - without knowing what's going on under the hood
4. Looking under the hood - at least a little
5. Tweaking your visualization

### 1. Identifying a place in which to work
This one's entirely on you! You need to find a place (i.e., a folder) on your PC or 
your favorite file server in which to store your visualization work.
For the sake of simplicity, I'll refer to this location as __viz\_home__.
You should substitute the actual path to the place where you'll be working.

### 2. Creating a web server
If you have Python installed on your PC \(and if you've followed the instructions and have
gotten this far, it is\) __you have a webserver installed on your PC!__ \(Betcha didn't know that.\)
Granted, this isn't a full-featured webserver (it can't serve video, for example) and is pretty 
much limited to serving HTML to yourself - but this is all you need to get started developing
visualizations with plotly \(and indeed, with web development in general.\)

Let's launch your webserver, and verify that it's working.

In order to do this,run:
```
Start->Anaconda (64-bit) -> Anaconda Prompt (anaconda3)
```
A command-box will appear. In the command box, __cd__ into your __viz\_home__:
```
cd viz_home
```
Your __viz\_home__ will be the root directory of the webserver you'll now launch.  
Enter the following command in the command box to launch your webserver:
```
python -m http.server 8888
```
The __8888__ parameter in the command you just entered is the number of the __port__ on which
your webserver will be "listening for traffic", i.e., listening for requests to display a web page \(in our
case, display a data visualizaiton\).

Let's make sure our webserver is working. To do this:
1. Download the __index.html__ page from this repository, and save it in your __viz\_home__.
2. Download the __index2.html__ file from this repository, and save it in your __viz\_home__.
3. Open a new tab in your web browser, and enter the following in the address bar:
```
http://localhost:8888
```
If you've done everyting correctly thus far, you'll see a page displaying the text "Hello, world!"

Notes: 
1. The __localhost__ in the URL you just enetered refers to the webserver that you just launched on your PC (your "local host machine".)
2. The __8888__ is the number of the port on which the webserver is listening for requests.
3. By default, this webserver (and most webservers, in general\) are configured to render the page named __index.html__ in their "root" directory.

However, you can request a page in the root directory explicitly. Try entering the following in the address bar of your web browser:
```
http://localhost:8888/index.html
```
The very same page will be displayed.  
Now try:
```
http://localhost:8888/index2.html
```
And you'll see that a different page is now displayed.

### 3. Creating your first visualization
Our first visualization will be a pie chart displaying transportation mode share data for the City of Boston between 1990 and 2014.
The data for this visualization is obviously pre-pandemic, so bear this in mind.

Let's the HTML page with this visualization into your web browser \(don't worry, all the work has already been done for you\),
and take a look at it.
First, download the file __first\_visualizaiton.html__ into your __viz\_home__ folder, and open it in a tab in your web browser:
```
http://localhost:8888/first_visualization.html
```
Not bad, and it's displaying genuinely useful information to boot.
There are many cases in which this sort of visualization would do the job nicely.
Some of these might include:
1. mode-share data (of course)
2. TIP project funding breakdowns
3. demographic breakdowns
4. and so on.

Let's next look under the hood to understand how this visualization works,
how it can be tweaked, and how we can generate the same kind of pie chart 
using a different dataset.

### 3. Looking under the hood
Open the file __first\_visualization.html__ in your chosen text editor.

### 4. Tweaking your visualization




## Plotly visualization 102 - visualation templates

