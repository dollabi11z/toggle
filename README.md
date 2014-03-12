JW Player Toggle
==========

This is a small example for use with the JW Player. It allows visitors of the website to select which rendering mode they want to view the player in - Flash or HTML5. It adds a dock button to the player with this toggle. The choice is saved as a cookie.

### [Demo](http://www.pluginsbyethan.com/github/toggle.html)

Implementation:
==========

You need the following script above your JW Player embed instance:

<pre>
var primary = 'html5';
var thecookies = document.cookie.split(&quot;;&quot;);
for (i=0; i &lt; thecookies.length;i++){
	var x = thecookies[i].substr(0,thecookies[i].indexOf(&quot;=&quot;));
	var y = thecookies[i].substr(thecookies[i].indexOf(&quot;=&quot;)+1);
	x = x.replace(/^\s+|\s+$/g,&quot;&quot;);
	if (x == 'primary') {
		primary = y;
	}
}
</pre>

Then, embed the player. One note here is that you must set the player's primary option to the variable we created in the first step (called primary), as that is what the script is looking for whe then toggle button is pressed:

<pre>
jwplayer(&quot;player&quot;).setup({
	file: 'http://content.bitsontherun.com/videos/bkaovAYt-injeKYZS.mp4',
	image: 'http://content.bitsontherun.com/thumbs/bkaovAYt-480.jpg',
	title: 'Big Buck Bunny',
	primary: primary
});
</pre>

Then, after your JW Player embed instace, this is needed as well:

<pre>
jwplayer().onReady(function(){
	if(jwplayer().getRenderingMode() == &quot;flash&quot;){
		this.addButton(&quot;html5.png&quot;, &quot;Switch to HTML5&quot;, switchIt, &quot;button1&quot;);
	} else {
		this.addButton(&quot;flash.png&quot;, &quot;Switch to Flash&quot;, switchIt, &quot;button1&quot;);
	}
});
function switchIt(){
	primary == 'html5' ? primary = 'flash': primary = 'html5';
	document.cookie = &quot;primary=&quot; + primary;
	window.location.reload();
};
</pre>

There are two png files that are needed that have to reside on your web server, html5.png, and flash.png. Please make sure to upload them and reference them in your script accordingly.

Full Example:
==========
<pre>
&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;title&gt;Toggle&lt;/title&gt;
&nbsp;&nbsp;&nbsp;&nbsp;&lt;script type=&quot;text/javascript&quot; src=&quot;http://p.jwpcdn.com/6/8/jwplayer.js&quot;&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;style type=&quot;text/css&quot;&gt;
	body { 
		margin: 0; 
		padding: 0; 
	}
&lt;/style&gt;
&lt;body&gt;
&lt;div id=&quot;player&quot;&gt;&lt;/div&gt;
&lt;script type=&quot;text/javascript&quot;&gt;
var primary = 'html5';
var thecookies = document.cookie.split(&quot;;&quot;);
for (i=0; i &lt; thecookies.length;i++){
	var x = thecookies[i].substr(0,thecookies[i].indexOf(&quot;=&quot;));
	var y = thecookies[i].substr(thecookies[i].indexOf(&quot;=&quot;)+1);
	x = x.replace(/^\s+|\s+$/g,&quot;&quot;);
	if (x == 'primary') {
		primary = y;
	}
}
jwplayer(&quot;player&quot;).setup({
	file: 'http://content.bitsontherun.com/videos/bkaovAYt-injeKYZS.mp4',
	image: 'http://content.bitsontherun.com/thumbs/bkaovAYt-480.jpg',
	title: 'Big Buck Bunny',
	primary: primary
});
jwplayer().onReady(function(){
	if(jwplayer().getRenderingMode() == &quot;flash&quot;){
		this.addButton(&quot;html5.png&quot;, &quot;Switch to HTML5&quot;, switchIt, &quot;button1&quot;);
	} else {
		this.addButton(&quot;flash.png&quot;, &quot;Switch to Flash&quot;, switchIt, &quot;button1&quot;);
	}
});
function switchIt(){
	primary == 'html5' ? primary = 'flash': primary = 'html5';
	document.cookie = &quot;primary=&quot; + primary;
	window.location.reload();
};
&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

The source code is available for this example. There is just a .html file. Publishing the html can be simply done with any text editor. Enjoy~! :)
