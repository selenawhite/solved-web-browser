Download Link: https://assignmentchef.com/product/solved-web-browser
<br>
Write a very simple GUI web browser. Your program should have a text edit box at the top of the window for the user to type a URL. Provide a listener that activates when the user types something in and presses “Enter”.

The HTTP specification is fairly simple. Create a <code>Socket</code> object from the URL’s web address, connecting on port 80 (the default HTTP port). You will probably want to attach a <code>PrintWriter</code> and a <code>BufferedReader</code> to the <code>Socket</code>. Send the following lines of text, ending in both carriage return and newline characters (yes, HTTP follows Windows line-ending conventions, rather than Unix):

<pre><code>GET &lt;filepath&gt; HTTP/1.1Host: &lt;web address&gt;&lt;blank line&gt;</code></pre>

In other words, if the user typed <code>http://cs.okstate.edu/students.html</code>, your program should send these three lines to the <code>Socket</code>:

<pre><code>GET /students.html HTTP/1.1r
Host: cs.okstate.edur
r
</code></pre>

Don’t forget to flush your output afterwards, or your request will never be sent. The web server will respond with a bunch of text including the web page, which you should read into a <code>String</code>. In the program panel, display (as plain text) the body of the webpage (explained below). Make sure that you set up the display so that it includes a scroll bar when needed. You must also handle exceptions and errors gracefully. If the user enters a nonexistent URL, for instance, or if the HTTP response is formatted incorrectly, then the program should inform the user.

A proper HTTP response will look like the following:

<pre><code>HTTP header junkSeveral linesUser doesn’twant to see this stuff&lt;html some other formatting&gt;&lt;head maybe some additional stuff&gt;Javascript definitionsOther stuff the user doesn’t care about.&lt;title&gt;The Title of the Webpage&lt;/title&gt;&lt;/head&gt;&lt;body onload="main()" might be telling the browser to run Javascript&gt;Here’s all the stuff the user really cares about.&lt;h1&gt;Along with a bunch of formatting,&lt;/h1&gt;&lt;a href="http://another.webpage.org"&gt;links,&lt;/a&gt;&lt;img src="http://another.webpage.org/lolcat.jpg" and some other image info&gt;and images.&lt;/body&gt;&lt;/html&gt;</code></pre>

Browsers display HTML by following the instructions provided by tags delineated by angle brackets. The first word inside a bracket specifies the kind of tag; tags can then have other information inside, and then end with a closing bracket. All of the text after a tag is formatted according to the tag’s instructions, until a closing tag is encountered. These tags are also delineated by angle brackets, and include a slash and then the name of the tag. Thus, in the example, the line “Along with a bunch of formatting,” is enclosed by the “h1” tag, which instructs the browser to display it with a font size indicating that it is a first-level heading. According to the HTML specification, browsers are not required to implement all of the scores of tags that exist, and they should ignore any tags they do not recognize. Your browser will ignore almost all of them.

It will be able to do the following:

<ul>

 <li>Extract the webpage’s title from between the <code>&lt;title&gt;</code>and <code>&lt;/title&gt;</code> tags and change the title of your program frame appropriately.</li>

 <li>Display all of the text located between the <code>&lt;body ...&gt;</code> and <code>&lt;/body&gt;</code> tags, and nothing outside of the body.</li>

 <li>Ignore every other tag. Don’t print out any angle brackets or any of the text located inside of them.</li>

</ul>

Needless to say, once you have the webpage loaded into a String, you will be using a lot of <code>substring()</code> and <code>charAt()</code> calls to massage the response into the webpage you will display to the user.

Note: Java has a few interesting classes that will render HTML themselves, such as the <code>JEditorPane</code>.

They’re fun to play around with, and might even be useful to you as a first step to getting your program working. However, for the purposes of this assignment, you must implement your own simple renderer, working from the simple string of plain text you get from a web server.

Note: More and more web pages are using the encrypted “Secure HTTP” protocol, which is denoted “https” in the URL. Your browser will be unable to access these web pages (including common ones like google.com). Don’t assume your browser is broken when testing your code until you have verified that you are not trying to access an encrypted page.

<strong>Extra Credit:</strong> Implement another few HTML tags. Some suggestions: Headings (<code>&lt;h1&gt;</code>, <code>&lt;h2&gt;</code>, etc) should change the font size. Images (<code>&lt;img src=URL&gt;</code>) could be displayed via <code>Toolkit.getImage(URL)</code>. Hyperlinks (<code>&lt;a href=URL&gt;</code>) could be implemented as buttons or clickable text (this is nontrivial, but it would make your browser into a true websurfing app, which would be pretty cool).