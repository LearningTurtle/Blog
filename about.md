---

layout: page
title:  ""

---
<div >
  <br>
<div style="margin-left:100px; margin-right: 100px; ">

We are Tejas and Nikhil !

<br>
We are currently Undergrad at IIT, kharagpur
We are budding Researcher and interested in Educating People about machine learning concepts.<br>
Here we are documenting about to Intuitive explanation of machine learning concepts.
<br>
send us an email on "learningturtleyt@gmail.com"
</div>
<br>
<br>
<br>
<div style="text-align:center;font-size: 30px">
<b>	
CONTECT US
</b>

</div>

<div style="text-align:center;font-size:150%;">
<br>

  {% if site.ajaxify_contact_form %}
    <form class="form-stacked">
      <label>
        Email
        <input type="text" name="email" class="field-light" placeholder="{{ site.text.contact.email | default: "Email Address" }}">
      </label>
        <br>

      <label>
        Content
        <textarea type="text" name="content" class="field-light" rows="5" placeholder="{{ site.text.contact.content | default: "What would you like to say?" }}" style="resize: vertical"></textarea>
      </label>

      <input type="text" name="_gotcha" style="display:none" />

      <button type='submit' class="button button-blue button-big mobile-block">{{ site.text.contact.submit | default: "Say Hello" }}</button>
    </form>
  {% else %}
    <form action="https://formspree.io/myynpjpw" method="POST" class="form-stacked">
      <label>
        Email
        <br>
        <input type="text" name="email" class="field-light" placeholder="{{ site.text.contact.email | default: "Email Address" }}">
      </label>
      <br>
      <label>
        Content
        <br>
        <textarea type="text" name="content" class="field-light" rows="5" placeholder="{{ site.text.contact.content | default: "What would you like to say?" }}" style="resize: vertical"></textarea>
      </label>

      <input type="hidden" name="_next" value="{{ site.baseurl }}/thanks/" />
      <input type="hidden" name="_subject" value="{{ site.text.contact.subject | default: "New submission!" }}" />
      <input type="text" name="_gotcha" style="display:none" />
      <br>
      <input type="submit" class="button button-blue button-big mobile-block" value="{{ site.text.contact.submit | default: "Say Hello" }}">
    </form>
  {% endif %}

 {% if site.ajaxify_contact_form %}
  {% include ajaxify_content_form.html %}
{% endif %}
</div>
<br>
<br>
<br>
<div align="center">
  <i>
  © 2020 Learning Turtle
  </i>
</div>>