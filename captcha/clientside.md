# Clientside (Google re-captcha)
1. Register site in Google first
2. Copy private key and public key


### PHP Server code
```
// formhandler code
$privatekey = '6LexH1IUAAAAAM6IpXaqxp21Fme83uapwWYDqAjh';

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "https://www.google.com/recaptcha/api/siteverify");
curl_setopt($ch, CURLOPT_HEADER, 0);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, [
    'secret' => $privatekey,
    'response' => $_POST['g-recaptcha-response'],
    'remoteip' => $_SERVER['REMOTE_ADDR']
]);
$resp = json_decode(curl_exec($ch));
curl_close($ch);
if ($resp->success) {
	// handle successful captcha
}
```

### Clientside code
```
<!-- place on head -->
<script src="https://www.google.com/recaptcha/api.js" async defer></script>

<!-- put inside form -->
<p align="center">
  <div class="g-recaptcha" data-sitekey="6LexH1IUAAAAABpjxcFS1pMkbstBEU_MSEppy-H-" style="transform:scale(0.77);-webkit-transform:scale(0.77);transform-origin:0 0;-webkit-transform-origin:0 0;"></div>
</p>
```

