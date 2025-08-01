---
layout: default
title: Contact
permalink: /contact/
description: Send us a mail
---

# Send us a message

<form action="https://getform.io/f/avrylzea" method="POST" enctype="multipart/form-data">
    <input type="text" name="name" placeholder="Name">
    <br/>
    <input type="email" name="email" placeholder="Mail">
	<br/>
	<input type="subject" name="subject" placeholder="Subject">
    <br/>
    <textarea rows="10" cols="25" name="message" placeholder="Message"></textarea>
   <br/>
    <input type="file" name="file">
   <!-- add hidden Honeypot input to prevent spams -->
   <br/>
    <input type="hidden" name="_gotcha" style="display:none !important">
   <br/>
    <button type="submit">Send</button>
</form>
