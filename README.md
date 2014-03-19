Authentication and Authrization Module for PHPixie
====================

Auth supports logging the user via:

* Login/Password authentication, passwords are automatically hashed and salted
* Facebook login

Role drivers allow you to configure roles based on either an ORM relationship or a field in the users table.

To use this module:

* Put it in your /modules folder
* Add 'auth' to modules array in /application/config/core.php
* Read about how to use it here [http://phpixie.com/modules/auth-module/](http://phpixie.com/modules/auth-module/)

Add a config file under */assets/config/auth.php*

	return array(
	    'default' => array(
	        'model' => 'user',	//Name of the users table
	        'login' => array(
	            'password' => array(
	                'login_field' => 'username',
	                //Must be minimum 50 characters long in database
	                'password_field' => 'password',
	                'remember_me_field' => 'remember_me',
					'remember_me_lifetime' => 63072000,	//60s * 60min * 24h * 365d * 2y
					'secret_key' => 'rqgF6cwqLrwmWfxDquC7',	//Secret key used to hash the remember_me cookie
					'allow_multiple_login' => true	//User can login with different browsers/computers at the same time
	            ),
	            'facebook' => array(
	                //Facebook App ID and Secret
	                'app_id' => '138626646318836',
	                'app_secret' => '49451a54b61464645321d9fbcb70000',
	                //Permissions to request from the user
	                'permissions'  => array('user_about_me'),
	    			'fbid_field' => 'fb_id',
	                //Redirect user here after he logs in
	                'return_url' => '/fairies'
	            )
	        ),
	        //Role driver configuration
	        'roles' => array(
	            'driver' => 'relation',
	            'type' => 'has_many',
	            //Field in the roles table
	            //that holds the models name
	            'name_field' => 'name',	//Column for the name of the roles
	            'relation' => 'roles'	//Name of the role table
	        )
	    )
	);