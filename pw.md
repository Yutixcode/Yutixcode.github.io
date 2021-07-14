---
layout: page
title: Your Password
---

Password ini tidak permanen dan akan berganti setiap waktu yg ditentukan.
<div id="is"></div>
Kalo lu mau yg tanpa password, tinggal chat gua aja.

<script src="https://utteranc.es/client.js"
  repo="Yutixcode/Yutixcode.github.io"
  issue-term="{{ page.title }}"
  theme="boxy-light"
  crossorigin="anonymous"
  async>
</script>

<script type="text/javascript">
  const queryString = window.location.search;
  const urlParams = new URLSearchParams(queryString);
  const yo = urlParams.get('pw');
  
  if (yo.length == 32) {
    document.getElementById("is").innerHTML += "<pre><code>"+yo+"</pre></code>";
  } else if (yo == null) {
    window.location.href = "/";
  } else {
    alert("Lu heker ya bang?");
    window.location.href = "/";
  }
</script>
