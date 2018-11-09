
#### Custom Password Form
We will first alter the password protected form. The structure of form can be changed as according to your need.
```sh
function custom_password_form() {
global $post;
$label = 'pwbox-'.( empty( $post->ID ) ? rand() : $post->ID );

$response = '<div class="passowrd-protected-wrapper">
<form class="protected-post-form" action="'.get_site_url().'/wp-login.php?action=postpass" method="post">
<h1 class="pass-protc-head">'. __( "Password Protected", 'theme_domain' ) . '</h1>
<label class="pass-label" for="' . $label . '">' . __( "To view this protected page, enter the password below:", 'theme_domain' ) . ' </label>
<input name="post_password" id="' . $label . '" type="password" />
<input type="submit" name="Submit" class="button" value="' . esc_attr__( "Submit", 'theme_domain' ) . '" />
</form>
</div>';

return $response;
}
add_filter( 'the_password_form', 'custom_password_form' );
```
#### Error Message
WordPress doesn't show error message by default but we are going to generate a custom error message on login failure.
```sh
function custom_password_form_err( $form ) {
if ( ! isset ( $_COOKIE[ 'wp-postpass_' . COOKIEHASH ] ) ) {
		return $form;
}

$msg = esc_html__( 'Sorry, your password is wrong.', 'theme_domain' );
$msg = "<p class='custom-password-message'>$msg</p>";
unset($_COOKIE[ 'wp-postpass_' . COOKIEHASH ]);
setcookie('wp-postpass_' . COOKIEHASH, null, -1, '/');
 return $msg . $form;
}

add_filter( 'the_password_form', 'custom_password_form_err' );
```
#### Custom Form Styling
I will leave you to do this part as you desire. You just need to add your css in theme.
