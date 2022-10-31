# Project 7 - WordPress Pen Testing

Time spent: 4 days spent in total

> Objective: Find, analyze, recreate, and document **Three vulnerabilities** affecting an old version of WordPress

## Pen Testing Report
### Scan
This is a scan done with WordPress version 4.0 and the reflex-gallery plugin. Using WPScan with a Kali linux OS in Virtual Box the scan shows 112 Vulnerabilities. 

<img src="WPScan.gif" width="600">

### 1. Admin XSS

- [ ] Summary: 
  - Vulnerability types: Cross-Site Scripting (XSS)
  - Tested in version: Word Press 4.0
  - Fixed in version: 4.6.1
- [ ] GIF Walkthrough:
<img src="XSS Attack.gif" width="600">
- [ ] Steps to recreate:
Here the admin will be logged in creating a page for the end-users. While the admin creates this page they can hide a XSS script such as the one below for them to click. That can then execute the injections and cause future harm.

```
<a href="></a><a title=" onClick=alert('Well_hello_there') "> Nature</a>
```

- [ ] Affected source code:
  - [Link 1]([[https://core.trac.wordpress.org/browser/tags/version/src/source_file.php](http://wpdistillery.vm/%3E%3C/a%3E%3Ca%20title=)]

### 2. (Required) Vulnerability Name or ID

- [ ] Summary: 
  - Vulnerability types: Click Jacking
  - Tested in version: 4.0
  - Fixed in version: Im not sure
- [ ] GIF Walkthrough:

<img src="Clickjacking.gif" width="600">

- [ ] Steps to recreate: 

Clickjacking can be used to redirect the end-user somewhere else using a link or image. This attack is also considered part of the XSS family but it is also known as "hijack clicking". In the first attack it imitate a link that the end-user will click on. From there the threatactor will be able to looking into thier cookie sessions and steal any assets the user may have. The second attack shows an image that has a hidden link. If the image was suppose to imitate a video the target will click on it initating what ever attack may happen. In this case it the target was redirected to a new webpage. 

```
<html>
	<head>
		<title>ClickJack</title>
	<head>
	<body>
	<iframe src="https://mrdoob.com/projects/chromeexperiments/google-gravity/" onmouseover= alert(document.cookie);></iframe>
	<body>
```

```
<a href="https://mrdoob.com/projects/chromeexperiments/google-gravity/" rel="nofollow"><img src="data:image/jpeg;base64,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"></a>
```

- [ ] Affected source code:
[Link 1](http://wpdistillery.vm/bio/)

### 3. Arbitrary File Upload

- [ ] Summary: 
  - Vulnerability types: XSS
  - Tested in version:4.0
  - Fixed in version: 
- [ ] GIF Walkthrough:

<img src="Arbitrary File Upload.gif" width="600">

- [ ] Steps to recreate: 
This exploit was already discovered back in `2015-03-08` by `Anant Shrivastava`. However I though this was good to point out again because this exploit did show up on my WPScan from the relfex-gallery plugin, verion 1.3.3, and I will be recreating the attack. What makes this exploit harmful is from the plugin itself. The reason is this plugin and I'm sure others opens up a hole allowing the threatactor to inject a XSS code. Once injected the threatactor is able to upload any type of file to the webpage causing unknown harm; all because the application fails to sanitize the input.

``` 
<form method = "POST" action = "" enctype = "multipart/form-data" >
<input type = "file" name = "qqfile"><br>
<input type = "submit" name = "Submit" value = "inurl">
</form >

```

- [ ] Affected source code:
  - [Link 1](http://wpdistillery.vm/food/#comment-11)


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)
- [PortSwigger XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
- [A story of forgotten disclosure and DOM XSS](https://blog.anantshri.info/forgotten_disclosure_dom_xss_prettyphoto)

GIFs created with  ...
[ScreenToGif](https://www.screentogif.com/) for Windows

## Notes
Challenges that I encountered was understanding the instructions since they were not as clear until a TA had explained them to me.

## License

    Copyright [yyyy] [Francisco Frade]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
