# Standard Bootstrap Contact Form

```
<form class="main-form">
  <div class="form-group">
    <label for="firstname" class="sr-only">First Name</label>
    <input type="text" class="form-control" placeholder="First Name" id="firstname" name="firstname" required>
  </div>
  <div class="form-group">
    <label for="lastname" class="sr-only">Last Name</label>
    <input type="text" class="form-control" placeholder="Last Name" id="lastname" name="lastname" required>
  </div>
  <div class="form-group">
    <label for="businessname" class="sr-only">Business Name</label>
    <input type="text" class="form-control" placeholder="Business Name" id="businessname" name="businessname" required>
  </div>
  <div class="form-group">
    <label for="phone" class="sr-only">Phone Number</label>
    <input type="phone" class="form-control" placeholder="Phone" id="phone" name="phone" required>
  </div>
  <div class="form-group">
    <label for="email" class="sr-only">Email</label>
    <input type="email" class="form-control" placeholder="E-mail" id="email" name="email" required>
  </div>
  <p align="center">
    <div class="g-recaptcha" data-sitekey="" style="transform:scale(0.77);-webkit-transform:scale(0.77);transform-origin:0 0;-webkit-transform-origin:0 0;"></div>
  </p>
  <button class="btn btn-success btn-block btn-lg btn-orange" style="margin-top:15px">Submit</button>
  <div class="alertdiv"></div>
</form>
```

```
$('.main-form').submit(function(e) {
      e.preventDefault();
      var data = $(this).serialize(),
          alertdiv = $(this).find('.alertdiv');
      console.log(data);
      $.ajax({
        url: '/formhandler.php',
        data: data,
        dataType: 'json',
        type: 'POST'
      }).done(function(d) {
        alertdiv.html('<div class="green">We got your contact details. A consultant will call you in 24 hours. Thank You</div>');
        alertdiv.slideDown();
      }).fail(function() {
        alertdiv.html('<div class="red">There was an error in your submission. Please make sure ReCaptcha is done correctly</div>');
        alertdiv.slideDown();
      });
    });
```