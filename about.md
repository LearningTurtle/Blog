---

layout: page
title:  about

---
<p align="center">

We are budding Developer, Researcher and Educator.
<br>
On the quest to  fill the gap of crucial Concept often remain unanswer
</p>


<br>
<div style="text-align:center;">
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
