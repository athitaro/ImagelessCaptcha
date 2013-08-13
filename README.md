# Imageless Captcha

## Advantages

* Keeps your form clean, no ugly captcha images or third-party embedded styles
* Extremely lightweight
* Very easy to implement
* Customizable

## [Try the demo](http://inorganik.net/imagelessCaptcha)

## How it works

Creates a random number on every page load, based on your preferences. From that number, it creates the number as a phrase. In the form, you use the phrase to ask the user to enter it as a number. When the form is posted, you simply check to see if the number matches.

## Setup

Include the imagelessCaptcha class:
```php
<?php include "imagelessCaptcha.php"; ?>
```

Implement the class

```php
<?php
$imgLess = new imagelessCaptcha();
$intPhrase = $imgLess->formPhrase();
$int = $imgLess->getInt();
?>
```

In your form, add a section for the Imageless Captcha:

1. echo the number phrase in a form label
2. add a field for number input
3. add a hidden field with the correct number

Be sure to add the `step` attribute to the number field if you enable decimals.

```php
<label>Imageless Captcha (spam filter):<br>
<?php echo $intPhrase; ?></label>
<input type="number" name="number" step="0.1">
<input type="hidden" name="correctNumber" value="<?php echo $int; ?>">
```

On post submit, check user submitted number against the correct number:

```php
if (isset($_POST['submit'])) {
	...
	// users attempt
	$number = intval($_POST['number']);
	// get correct number from hidden field
	$correctNumber = intval($_POST['correctNumber']);

	$errors = array();

	// check user-submitted number against correct number
	if ($number != $correctNumber) {
		$errors['captcha'] = "The number you entered for the spam filter is incorrect.";
	}
	if (!$errors) {
		// do something here
	} 
}
```

## Customize

In `imagelessCaptcha.php`, simply edit the preferences array:

```php
// set preferences
private $prefs = array(
	
	'num_digits' => 3, // 1 - 4
	
	'use_decimal' => true, // adds a decimal to the number
	
	'decimal_chance' => true // makes whether a decimal is added random
);
```

## Contribute

Fork this repo and add more language support!

