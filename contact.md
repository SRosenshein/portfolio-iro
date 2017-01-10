---
layout: page
title: Contact
permalink: /contact/
feature-img: "img/sample_feature_img_3.png"
---
Send me a message saying hi! 

<form action="https://getsimpleform.com/messages?form_api_token=dc07c2c82893ae840022bc956f88acb0" method="post">
  <!-- the redirect_to is optional, the form will redirect to the referrer on submission -->
  <p>
	  <input type='hidden' name='redirect_to' value='http://sam-rosenshein.com/thank-you/' />
	  <input type='text' name='name' placeholder='Your Full Name' />
	  <input type='email' name='email' placeholder='Your E-mail Address' />
	</p>
  <textarea name='message' rows='7' cols="80" placeholder='Write your message ...'></textarea>
  <br/>
  <input type='submit' value='Send Message' />
</form>