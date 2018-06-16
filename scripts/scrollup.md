# Scrollup Animation
jQuery animation to top

### HTML
```
<div class="scrollup">
  <i class="fa fa-chevron-up"></i>
</div>
```

### CSS
```
.scrollup {
    width: 40px;
    height: 40px;
    line-height: 40px;
    text-align: center;
    color: #ffffff !important;
    background: #7497ab;
    position: fixed;
    bottom: 20px;
    right: 30px;
    z-index: 9999;
    cursor: pointer;
}
```

### JS
```
$('.scrollup').click(function() {
    $('html, body').animate({
        scrollTop: 0
    }, 500);
});

$('.scrollup').hide();

// fade effect if on top
$(window).scroll(function () {
    if ($(this).scrollTop() > 5) {
            $('.scrollup').fadeIn();
    } else {
        $('.scrollup').fadeOut();
    }
});
```
