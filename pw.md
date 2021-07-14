---
layout: page
title: Your Password
---

Password ini tidak permanen dan akan berganti setiap waktu yg ditentukan.
<div id="is"></div>
<script type="text/javascript">
  const queryString = window.location.search;
  const urlParams = new URLSearchParams(queryString);
  const yo = urlParams.get('pw');
  
  if (yo.length == 32) {
    document.getElementById("is").innerHTML += "<pre><code>"+yo+"</pre></code>";
  } else if (yo == null) {
    window.location.href = "/";
  } else {
    alert("Mau ngapain nyet?");
    window.location.href = "/";
  }
</script>
