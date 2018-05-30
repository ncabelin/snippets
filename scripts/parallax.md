# Parallax effect

### HTML
```
<section class="parallax" data-speed="2">
</section>
```


### JS
```
$('.parallax').each(function(){
    var $bgobj = $(this); // assigning the object
    
    $(window).scroll(function() {
    
        // Scroll the background at var speed
        // the yPos is a negative value because we're scrolling it UP!                              
        var yPos = -($window.scrollTop() / $bgobj.data('speed'));
        
        // Put together our final background position
        var coords = '50% '+ yPos + 'px';
        
        // Move the background
        $bgobj.css({ backgroundPosition: coords });
        
    }); // end window scroll
});
```