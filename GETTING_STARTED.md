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
Our first visualization will be a pie chart displaying
[transportation mode share data for the City of Boston between 1990 and 2014](https://www.boston.gov/sites/default/files/file/document_files/2017/03/go_boston_2030_-_3_boston_today_spreads.pdf).
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
Like all HTML files, it's top level strucutre: it consists of a \<head\> and a \<body\> tag.
Let's take a look at the contents of each of these, drilling down for detail when appropriate.

#### The \<head\> tag
The contents of the \<head\> tag are:
```
<head>
	<!-- Load plotly.js library from a CDN -->
	<script src='https://cdn.plot.ly/plotly-2.20.0.min.js'></script>
</head>
```
All that's going on here is that the web browser is being told to download the source code for the plotly 
JavaScript library from a Content Delivery Network (CDN), so it can be used subsequently to generate visualizations.
That's all there is to it.

#### The \<body\> tag
The contents of the \<body\> tag are divided into two parts:
1. a \<div\> tag, and
2. a \<script\> tag

##### The \<div\> tag
The \<div\> tag defines a rectangular space (a "block-level element" in web-lingo) on the web page into which our visualization will be placed.
A page can contain an arbitrary number of \<div\> elements. 
In order to tell our viz-generating code to place our visualization into __this__ \<div\>, we need some way to identify it.
This is accomplished by adding an __id__ property to the \<div\> tag. This is done as follows:
```
<div id='myDiv'> 
```
As you can see, the __id__ of this \<div\> is __myDiv__.

##### The \<script\> tag
The \<script\> tag contains executable JavaScript code \(really not all that much!\) to generate the visualization. 
Unlike the \<script\> tag in the \<head\> element, rather than pulling in JavaScript code from an external source,
this block of JavaScript code appears in-line.

This block of JavaSdript code has three parts:
1. definition of the data to be rendered and the type of chart to generate
2. definition of the dimensions of the \<div\> into which the chart will be rendered
3. a call to the plotly library to generate the viz-generating
Each of these sections is commented in the code, but we'll walk through each one in turn.

__The Data__  
The relevant code block:
```
var data = [{ 	values: [38.9, 34.0, 14.3, 5.7, 3.4, 2.4, 1.4],
				labels: ['Drive Alone', 'Transit', 'Walk', 'Carpool', 'WFH', 'Bike', 'Other'],
				type: 'pie'
           }];
```
Without going into the details of the JavaScript syntax used here (I'm happy to do so offline), 
you'll see that there are a pair of parallell arrays of values (mode-share percentages) and
labels associated with those values. So, for example, this dataset indicates that 34.0 percent 
of people used transit to commute in Boston in the period 1990-2014.
There is also an indication of the type of visualization to generate: a __pie__ chart.

__Dimensions of the Plotting Area__  
The relevant code block:
```
var layout = {	height: 800,
				width: 1000
             };
```
This piece of code defines a JavaScript Object (sorry, I couldn't resist) with two key-value pairs.
These specify the height and width of the \<div\> into which our viz will be generated. Hard-core web geeks
might ask why these dimensions aren't specified as properties of the \<div\> tag discussed above.
The answer is: no reason at all. These dimensions could alternatively be defined as properties
of the __myDiv__ \<div\>. Sometimes there is more than one way to accomplish a single thing.

__Generation of the Viz__  
The relevant code block (just a one-liner):
```
Plotly.newPlot('myDiv', data, layout);
```
Here, we call Plotly's __newPlot__ function to generate our pie chart. The three parameters passed to the newPlot call are:
1. the __id__ of the \<div\> into which to place the chart
2. the data to render
3. a definition of the layout of the \<div\>
That's it.  

Now that you've generated your first viz, the next step is to tweak it and find out what happens when we do so.

### 4. Tweaking your visualization
There are an almost unlimied number of ways in which the first visualization could be tweaked.
This tutorial focus on a few of the most common tweaks you might have in mind:
* Changing the size of the plot
* Changing data values and labels
* Changing colors
* Adding a title

After you become familiar with these, I recommend looking into the plotly API which gives the user
control over almost all aspects of the visualization:
* [plotly API figure reference](https://plotly.com/javascript/reference/index/)
* [plotly API function reference](https://plotly.com/javascript/plotlyjs-function-reference/)
* [plotly API events reference](https://plotly.com/javascript/plotlyjs-events/) - probably not for beginners
* [plotly API configuration options](https://plotly.com/javascript/configuration-options/)

Let's get going.
#### Changing the size of the plot
One of the most common things you might want to do is to change the size of a plot, so it fits
more elegantly into the page of which it will be a part. 
This is easy, given the code that's already in the __first\_visualizaiton.html__ file.

Make a copy of this file, and call it __change\_size.html__.
Open it in your text editor of choice, and examine the definition of the __layout__ variable:
```
var layout = {	height: 800,
				width: 1000
             };
```
Let's reduce the dimensions of the visualization by half:
```
var layout = {	height: 400,
				width: 500
             };
```
Save the file, and load __change\_size.html__ into your web browser:
```
http://localhost:8888/change_size.html
```

#### Changing data values and labels
Let's change the data values for our visualization to reflect our best guess at 
what the post-pandemic mode-share is. 
I'll use the following values in this example;
feel free to substitute your own: 
| Mode | Mode Share |
|------|------------|
| Drive alone | 20 |
| Transit | 25 |
| Walk | 10 |
| Carpool | 5 |
| WFH | 35 |
| Bike | 4 | 
| Other | 1 |

Make a copy of __first\_visualizaiton.html__, and call it __post\_pandemic.html__.
Change the definition of the __data__ variable as follows:
```
var data = [{ 	values: [20, 25, 10, 10, 5, 35, 4, 1],
				labels: ['Drive Alone', 'Transit', 'Walk', 'Carpool', 'WFH', 'Bike', 'Other'],
				type: 'pie'
           }];
```
While we're at it, let's change the label for the 'WFH' mode to 'Work from Home':
```
var data = [{ 	values: [20.0, 25.0, 10.0, 5.0, 35.0, 4.0, 1.0],
				labels: ['Drive Alone', 'Transit', 'Walk', 'Carpool', 'Work from Home', 'Bike', 'Other'],
				type: 'pie'
           }];
```
Save the file, and load it into your browser:
```
http://localhost:8888/post_pandemic.html
```
#### Changing colors
If you don't tell plotly the colors to use when generating a visualization, it will make a "best guess" of its own.
However, a software package's "best guess" is rarely what the user had in mind, so it's likelly you'll want to
specify the colors used in a visuation yourself.
This is done by specifying a __colors__ array in the __marker__ property of the data object in your visualization.
\(We've not encounterd the __marker__ property before.\)

For the sake of simplicity, let's say we'd like to use the seven 'colors of the rainbow' as our color palette.
This can be done as follows:
```
var data = [{ 	values: [38.9, 34.0, 14.3, 5.7, 3.4, 2.4, 1.4],
				labels: ['Drive Alone', 'Transit', 'Walk', 'Carpool', 'WFH', 'Bike', 'Other'],
				marker: { colors: [ 'red', 'orange', 'yellow', 'green', 'blue', 'indigo', 'violet'	] },
				type: 'pie'
           }];
```
Web standards provide a variety of ways to specify colors.
In this case we've identified each color by its [standard CSS name](https://www.w3.org/wiki/CSS/Properties/color/keywords).
You can also specify a color by a [hexadecimal or decimal RGB value](https://www.w3.org/wiki/CSS/Properties/color/RGB).
Please see the documentation if you'd like to use the 'RGB' method.

#### Adding a title
Finally, let's add a title to our visualization.
This is easy; all you have to do is add a __title__ property to the __layout__ variable:
```
var layout = {  height: 800,
				width: 1000,
				title: 'Boston Mode-share: 1990-2014'
             };
```
Make a copy of Make a copy of __first\_visualizaiton.html__, and call it __viz\_with\_title.html__.
Make the change given above in this file, save it, and load it into your browser:
```
http://localhost:8888/viz_with_title.html
```

### Next steps
You've been introduced to how to make a variety of changes to a plotly visualation - each change "in isloation."
At this point, I recommend that you spend some time combining a variety of changes in a single visualiation,
and maybe even trying one or two other ones, inspired by reading the plotly documentation.

## Plotly visualization 102 - visualation templates

### Pie chart
You're already familiar with creating a pie-chart visualization from working with __first\_visualizaiton.html__.
The __pie\_chart\_template.html renders a pie chart of the population of five cities and towns in the
core of the Boston region: Boston itself, Cambridge, Somerville, Brookline, and Newton.
This template includes a couple of features commonly desired in pie charts that are given 'default' 
behavior in __first\_visualizaiton.html__; they are:
 adds a few features that might commonly be desired:
* control of the labels for each sector of the chart
* control of the on-hover tool tip for the sectors of the chart

Everything is bundled up nicely in the data object passed to plotly.
The relevant code reads as follows:
```
var data = [{ 	values: [617594, 105162, 75754, 58732, 85146],
				labels: ['Boston', 'Cambridge', 'Somerville', 'Brookline', 'Newton'],
				type: 'pie',
				textinfo: 'label+percent',				// Show label and percentage as the text for each sector of the pie chard
				hoverinfo: "label+value+percent"		// Show label, raw value, and percentage in on-hover tooltip
           }];
```

The __textinfo__ property specifies that the __label__ (i.e., the city or town name) for each sector and
the actual data __value__ (in this case, the population of the corresponding town) is diplayed in each sector
of the pie chart.

The __hoverinfo__ property specifies that the label, actual data value, and relative __percent__age is
shown in the 'on-hover' tooltip for this visualization.

### Bar chart
The template for bar charts __bar\_chart\_template.html__ renders a bar chart
that displays the weight of six candy bars (get it?) sold in the UK.
The data was taken from a page on the [Confectionary News](https://www.confectionerynews.com/Article/2015/11/13/Chocolate-bar-sizes-Historic-comparison-of-Hershey-s-and-Mars-bars)
website; the weight of the candy bars is given in grams.
This template includes labels for the x- and y-axes as well as a title for the viz as a whole.
Let's take a look at each interesting part of this viz.

The code block for the __data__ object is:
```
var data = [{ 	x: ["Kit Kat", "Mars", "Snickers", "Tiwx", "Reese's", "Hershey"],
                y: [45, 51, 48, 50, 42, 42],
				type: 'bar'
           }];
```
Unlike a pie chart, for which we supply an array of labels and an array of values, 
for a __bar chart__ we supply an array of x-axis values (most commonly, these are labels)
and an array of y-axis values. 
In this case, the x-axis values are the names of candy bars;
the y-axis values are the weight of each corresponding candy bar.

Labeling the axes of a bar chart is done by adding xaxis and yaxis properties
to the __layout__ object:
```
var layout = {  height: 800,
				width: 1000,
				title: 'Weight of Candy Bars in the UK',
				xaxis: { title: "Candy Bars (OK. We know Reese's isn't a candy bar, but this is just a template.)" },
				yaxis: { title: 'Weight in grams' }
             };
```
The __xaxis__ and __yaxis__ properties are themselves JavaScript objects, and each can contain many different properties.
In this case, all we need to do is to add a __title__ property to each one.

If we want to get fancy, we can specify the font for each axis's title.
Try the following on your own:
```
var layout = {  height: 800,
				width: 1000,
				title: 'Weight of Candy Bars in the UK',
				xaxis: { title: { 	text: "Candy Bars (OK. We know Reese's isn't a candy bar, but this is just a template.)",
									font: { family: 'Arial',
											 color:  'black',
											 size:   20
										   }
								}
						},
				yaxis: { title: {	text: 'Weight in grams',
									font: { family: 'Courrier',
											color:  'red',
											size: 	22
									}
								}
						}
             };
```
The result mightn't look all that great, but that's the point!
Feel free to play with the values of the font properties until the axis labels look nice.

### Line chart
Plotly allows multiple lines of data \(i.e., arrays of pairs of \[x,y\] values\) to be plotted together.
The __line\_chart\_template.html__ illustrates how to plot two lines in the same visualization,
but it can be easily extended to accommodate as many lines as needed.

Each line to be plotted is defined by its own JavaScript object. Let's take a look at the code
for the first one:
```
var line1 = {	x: [1, 2, 3, 4],
				y: [10, 15, 13, 17],
				mode: 'lines',
				name: 'Dataset 1'			// Name given to this line in the legend
};
```
The meaning of the arrays of __x__ and __y__ values should be obvious.
The value of the __mode__ property is critical: __lines__ instructs plotly to 
generate a line connecting the set of points rather than simply rendering the points.
The value of the __name__ property specifies the name of the line given in the 
visualization's legend.

As mentioned above, plotly allows an arbitrary number of lines to be plotted in the same 
visualization. 
Consequently, the data object passed to plotly when generating a line chart 
is an __array__ of objects defiing the line(s) to be plotted.
For example, the template defines two lines __line1__ and __line2__.
The data passed to Plotly.newPlot consequently is an array of these two objects:
```
var data = = [ line1, line2 ];
```
If you're only plotting a single line, you still have to pass an array as the data value.
In that case, the array would contain only a single value:
```
var data = = [ line1 ];
```

### Scatter plot
In the plotly world, scatter plots are very closely related to line charts.
The __scatter\_plot\_template.html__ consequently strongly resembles the __line\_chart\_template.html__.

The essential difference is the value of the __mode__ property in the JavaScript object
defining each array of values to plot.
When generating a scatter plot, the value of the __mode__ property is __markers__ rather than lines.
For example:
```
var points1 = {	x: [1, 2, 3, 4],
				y: [10, 15, 13, 17],
				mode: 'markers',			// Render points, do not connect points with lines
				name: 'Dataset 1'			// Name given to this line in the legend
};
```

As was the case for line plots, an array of objects defining each set of points to plot must be specified
as the data value passed to Plotly.newPlot. For example, to generate a plot of
three sets of points, you might write:
```
var data = [ points1, points2, points3 ];
```
Similarly, even if you have only one set of points to plot, you still must pass an array 
as the data parameter to Plotly.newPlot - again, an array containing one element:
```
var data = [ points1 ];
```

#### Getting a little fancy
The Plotly API for generating line plots and scatter plots is essentially the same.
The only difference is the value of the __mode__ property of the JavaScript object
that defines each set of points to plot.
If you guessed that you can combine a line plot and a scatter plot in the
same visualiation, your guess would be correct!

Consider giving the following a try:
```
var line = {	x: [1, 2, 3, 4],
				y: [10, 15, 13, 17],
				mode: 'lines',
				name: 'Dataset 1'
};
var points = {	x: [2, 3, 4, 5],
				y: [16, 5, 11, 9],
				mode: 'markers',
				name: 'Dataset 2'
};

var data = [ line, points ];

var layout = {  height: 800,
				width: 1000,
				title: 'Line chart + scatter plot',
				xaxis: { title: 'x-axis title' },
				yaxis: { title: 'y-axis title' }
             };

// The following statement generates the viz
Plotly.newPlot('myDiv', data, layout);
```

### Map

