# Animate scroll on click

```
$('.nav li a').click(function(e) {
  $('.navbar-toggle').trigger('click');
  var id = $(this).attr('href');
  e.preventDefault();
    $('html, body').animate({
        scrollTop: $(id).offset().top
    }, 500);
});
```