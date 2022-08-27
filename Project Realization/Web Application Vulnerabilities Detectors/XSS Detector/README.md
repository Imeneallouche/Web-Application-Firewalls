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
<br><br><br><br><br><br><br>

<h1 align="center">🌐 Demonstration 🌐</h1>
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
– Neutralizing the script when the HTML is output</p><br><br><br><br><br><br><br>




<h1 align="center">🌐 Get into The Attack 🌐</h1>

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

<br><p>• To perpetrate an XSS attack an attacker can use:</p>
<table>
  <tr>
    <td><b> A persistent attack</b></td>
    <td colspan='10'>where the data is permanantly located in a file system or database</td>
  </tr>
  
  <tr>
    <td><b>A non-persistent attack</b></td>
    <td colspan='10'>where the attack vector is inserted into the data stream but not stored</td>
  </tr>
</table>
  
 
