# VANILLA JAVASCRIPT / CSS

Enter CSS
```
/* The Modal (background) */
.n-modal {
    display: none; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0,0,0); /* Fallback color */
    background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content/Box */
.n-modal-content {
    background-color: #f3f4f5;
    margin: 15% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close-b {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
}

.close-b:hover,
.close-b:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}
```

Enter Modal HTML
```
<!-- The Modal -->
<div id="myModal" class="n-modal">

  <!-- Modal content -->
  <div class="n-modal-content">
    <span class="close-b">&times;</span>
  </div>
</div>
```

Enter JS
```
// Get the modal
	var modal = document.getElementById('myModal');

  // Get the button that opens the modal
	var btn = document.getElementById("payNow");

  // Get the <span> element that closes the modal
	var span = document.getElementsByClassName("close-b")[0];

  // When the user clicks on the button, open the modal
	btn.onclick = function() {
			$('.app-panel').hide();
			$('#panel-1').show();
	    modal.style.display = "block";
	}

  // When the user clicks on <span> (x), close the modal
	span.onclick = function() {
	    modal.style.display = "none";
	}

  // When the user clicks anywhere outside of the modal, close it
	window.onclick = function(event) {
	    if (event.target == modal) {
	        modal.style.display = "none";
	    }
	}
```
