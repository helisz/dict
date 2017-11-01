# PHP Cookies

### Set Cookies
```php
<?php

	add_action( 'init', 'setting_my_first_cookie' );

	function setting_my_first_cookie() {
	  setcookie( $v_username, $v_value, 30 * DAYS_IN_SECONDS, COOKIEPATH, COOKIE_DOMAIN );
	}

?>
```

### Get Cookies
```php
<?php

	if(!isset($_COOKIE[$v_username])) {
	  echo "The cookie: '" . $v_username . "' is not set.";
	} else {
	  echo "The cookie '" . $v_username . "' is set.";
	  echo "Cookie is:  " . $_COOKIE[$v_username];
	}

?>
```

#D elete Cookies
```php
<?php

  unset( $_COOKIE[$v_username] );
  setcookie( $v_username, '', time() - ( 15 * 60 ) );
  
?>

```