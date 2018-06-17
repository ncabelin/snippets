# Server Side captcha
Code taken from www.the-art-of-web.com

### Add to your Form
```
<form id="clientinfo">
   <div class="form-group">
     <input type="text" class="form-control" id="name" value="" placeholder="Name">
   </div>
   <div class="form-group">
     <input type="email" class="form-control" id="email" value="" placeholder="E-mail">
   </div>
   <div class="form-group">
     <input type="tel" class="form-control" id="phone" value="" placeholder="Phone">
   </div>
   <div class="form-group">
     <textarea class="form-control" id="message" rows="3" placeholder="Message"></textarea>
   </div>
   <!-- Captcha Code here -->
   <div class="center-block text-center">
     <p><img id="captcha" src="captcha.php" width="160" height="45" border="1" alt="CAPTCHA">
       <small><a href="#" onclick="
         document.getElementById('captcha').src = 'captcha.php?' + Math.random();
         document.getElementById('captcha_code').value = '';
         return false;
       " class="btn btn-xs btn-primary" id="refresh">refresh</a></small>
     </p>
     <p>
       <input id="captcha_code" type="text" name="captcha" size="6" maxlength="5" onkeyup="this.value = this.value.replace(/[^\d]+/g, '');" required>
       <small>copy the digits from the image into this box</small>
     </p>
   </div>
   <button class="btn btn-primary btn-sq btn-lg" type="submit" name="button">
       SUBMIT
   </button>
 </form>
```

### Create a php file `recaptcha.php`
Font files are required
```
<?php
  // Adapted for The Art of Web: www.the-art-of-web.com
  // Please acknowledge use of this code by including this header.

  // initialise image with dimensions of 160 x 45 pixels
  $image = @imagecreatetruecolor(160, 45) or die("Cannot Initialize new GD image stream");

  // set background and allocate drawing colours
  $background = imagecolorallocate($image, 0x66, 0xCC, 0xFF);
  imagefill($image, 0, 0, $background);
  $linecolor = imagecolorallocate($image, 0x33, 0x99, 0xCC);
  $textcolor1 = imagecolorallocate($image, 0x00, 0x00, 0x00);
  $textcolor2 = imagecolorallocate($image, 0xFF, 0xFF, 0xFF);

  // draw random lines on canvas
  for($i=0; $i < 8; $i++) {
    imagesetthickness($image, rand(1,5));
    imageline($image, rand(0,160), 0, rand(0,160), 45, $linecolor);
  }

  session_start();

  // using a mixture of TTF fonts
  $fonts = array();
  $fonts[] = "assets/fonts/R1.ttf";
  $fonts[] = "assets/fonts/R2.ttf";
  $fonts[] = "assets/fonts/R3.ttf";
  $fonts[] = "assets/fonts/O1.ttf";
  $fonts[] = "assets/fonts/O2.ttf";
  $fonts[] = "assets/fonts/O3.ttf";

  // add random digits to canvas using random black/white colour
  $digit = '';
  for($x = 10; $x <= 130; $x += 30) {
    $textcolor = (rand() % 2) ? $textcolor1 : $textcolor2;
    $digit .= ($num = rand(0, 9));
    imagettftext($image, 20, rand(-30,30), $x, rand(20, 42), $textcolor, $fonts[array_rand($fonts)], $num);
  }

  // record digits in session variable
  $_SESSION['digit'] = $digit;

  // display image and clean up
  header('Content-type: image/png');
  imagepng($image);
  imagedestroy($image);
?>
```
