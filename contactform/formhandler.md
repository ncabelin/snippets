# Mailing the form

```
		$firstname = $lastname = $email = $businessname = $phone = "";
    $recipient = "danny@crs.consulting";
    $firstname = test_input($_POST["firstname"]);
    $lastname = test_input($_POST["lastname"]);
    $email = test_input($_POST["email"]);
    $phone = test_input($_POST["phone"]);
    $businessname = test_input($_POST["businessname"]);

    $to = $recipient;
    $subject = "Request for Web Development";
    $msg = "<html>";
    $msg .= "<head>";
    $msg .= "</head>";
    $msg .= "<body>";
    $msg .= "<ul style='list-style:none; padding-left: 0'>";
    $msg .= "<li>First Name: $firstname</li>";
    $msg .= "<li>Last Name: $lastname</li>";
    $msg .= "<li>Phone: $phone</li>";
    $msg .= "<li>Email: $email</li>";
    $msg .= "<li>Business Name: $businessname</li>";
    $msg .= "</ul>";
    $msg .= "</body>";
    $msg .= "</html>";

    // Always set content-type when sending HTML email
    $headers = "MIME-Version: 1.0" . "\r\n";
    $headers .= "Content-type:text/html;charset=UTF-8" . "\r\n";
    $headers .= 'From: Quote Request <' . $recipient . '>' . "\r\n";

    if (mail($to,$subject,$msg,$headers)) {
      $success = true;
			$content = 'successfully posted';
			$response = array('Success' => $success, 'Content' => $content);
			header('Content-Type: application/json');
			echo json_encode($response);
    }
```