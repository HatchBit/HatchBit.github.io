---
title: お問い合わせ
subtitle: Contact us
layout: page
show_sidebar: false
permalink: /inquiry/
---

<!-- modify this form HTML and place wherever you want your form -->
<form id="my-form" action="https://formspree.io/f/mnqrdvng" method="POST">
    <div class="form-group">
        <label for="input-email" style="display: inline-block; width: 5rem;">Email:</label>
        <input type="email" name="email" id="input-email" class="form-control" style="width: 10rem;" />
    </div>
    <div class="form-group">
        <label for="input-message" style="display: inline-block; width: 5rem;">Message:</label>
        <textarea name="message" id="input-message" class="form-control" style="width: 10rem; height: 6rem;"></textarea>
    </div>
  <button id="my-form-button" class="btn btn-primary">送信</button>
  <p id="my-form-status"></p>
</form>
<!-- Place this script at the end of the body tag -->
<script>
    var form = document.getElementById("my-form");

    async function handleSubmit(event) {
      event.preventDefault();
      var status = document.getElementById("my-form-status");
      var data = new FormData(event.target);
      fetch(event.target.action, {
        method: form.method,
        body: data,
        headers: {
            'Accept': 'application/json'
        }
      }).then(response => {
        if (response.ok) {
          status.innerHTML = "お問い合わせありがとうございます！";
          form.reset()
        } else {
          response.json().then(data => {
            if (Object.hasOwn(data, 'errors')) {
              status.innerHTML = data["errors"].map(error => error["message"]).join(", ")
            } else {
              status.innerHTML = "メッセージ送信中に問題が発生しました"
            }
          })
        }
      }).catch(error => {
        status.innerHTML = "メッセージ送信中に問題が発生しました"
      });
    }
    form.addEventListener("submit", handleSubmit)
</script>