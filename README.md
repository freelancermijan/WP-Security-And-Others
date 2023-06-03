#### Checking breach passwords

    https://breachdirectory.org

#### WordPress Security Scan

    https://hackertarget.com/wordpress-security-scan/

#### WordPress Hide login page

    https://wordpress.org/plugins/wps-hide-login/

#### WordPress Complete Security

    https://wordpress.org/plugins/wordfence/
    pro https://mega.nz/file/WtcznApC#NwX6qnCj3w5AgShg7_zeSNeVrftdPRphukJzWzgk9CU

#### WordPress Captcha

    https://wordpress.org/plugins/simple-login-captcha/
    https://wordpress.org/plugins/login-recaptcha/
    https://wordpress.org/plugins/advanced-nocaptcha-recaptcha/

#### WordPress Http Header Security

    https://securityheaders.com/
    https://sitecheck.sucuri.net/
    https://www.webpagetest.org/
    https://domsignal.com/hsts-test

#### Headers Security Advanced Plugin
    https://wordpress.org/plugins/headers-security-advanced-hsts-wp/

    Features
    ● HSA Limit Login to block brute force attacks.
    ● X-XSS-Protection
    ● Expect-CT
    ● Access-Control-Allow-Origin
    ● Access-Control-Allow-Methods
    ● Access-Control-Allow-Headers
    ● X-Content-Security-Policy
    ● X-Content-Type-Options
    ● X-Frame-Options
    ● X-Permitted-Cross-Domain-Policies
    ● X-Powered-By
    ● Content-Security-Policy
    ● Referrer-Policy
    ● HTTP Strict Transport Security / HSTS
    ● Content-Security-Policy
    ● Clear-Site-Data
    ● Cross-Origin-Embedder-Policy-Report-Only
    ● Cross-Origin-Opener-Policy-Report-Only
    ● Cross-Origin-Embedder-Policy
    ● Cross-Origin-Opener-Policy
    ● Cross-Origin-Resource-Policy
    ● Permissions-Policy
    ● Strict-dynamic
    ● Strict-Transport-Security
    ● FLoC (Federated Learning of Cohorts)

#### Htaccess default code
    
    # BEGIN WordPress
    
    RewriteEngine On
    RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
    RewriteBase /
    RewriteRule ^index\.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]

    # END WordPress

#### Protecting .htaccess file itself

    # Protecting .htaccess file itself

    <files ~ “^.*\.([Hh][Tt][Aa])”>
    order allow,deny
    deny from all
    satisfy all
    </files>

#### Protecting wp-config.php file 

    # Protecting wp-config.php file

    <files wp-config.php>
    order allow,deny
    deny from all
    </files>

#### Protecting directory indexing

    # directory browsing block

    Options All -Indexes

#### Protecting xmlrpc.php file 

    #Disable XMLRPC.PHP

    <Files xmlrpc.php>
    order deny,allow
    deny from all
    </Files>

#### Disable scanners in Your Website

    # BEGIN block author scans

    RewriteEngine On
    RewriteBase /
    RewriteCond %{QUERY_STRING} (author=\d+) [NC]
    RewriteRule .* – [F]
    
    # END block author scans


#### Block Suspicious IP

    # IP block

    Order Allow,Deny
    Allow from all
    Deny from 1.186.48.58, 65.30.114.186, 69.143.222.95


#### Individual File Protection

    # Protect the .htaccess
    <files .htaccess="">
    order allow,deny
    deny from all
    </files>


#### wp-content Access Prevention

create a new `.htaccess` file in wp-content directory & put the code there

    # wp-content access deny

    Order deny,allow
    Deny from all
    <Files ~ “.(xml|css|jpe?g|png|gif|js)$”>
    Allow from all
    </Files>


#### Uploads Directory Access Blocking

create a new `.htaccess` file in wp-content/uploads directory & put the codes there

    # uploads directory access deny

    <Files *.php>
    deny from all
    </Files>
    # Block executables
    <FilesMatch “\.(php|phtml|php3|php4|php5|pl|py|jsp|asp|html|htm|shtml|sh|cgi|suspected)$”>
    deny from all
    </FilesMatch>

#### Secure wp-includes folder

    # Stop access from wp-include folder and files

    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^wp-admin/includes/ — [F,L]
    RewriteRule !^wp-includes/ — [S=3]
    RewriteRule ^wp-includes/[^/]+\.php$ — [F,L]
    RewriteRule ^wp-includes/js/tinymce/langs/.+\.php — [F,L]
    RewriteRule ^wp-includes/theme-compat/ — [F,L]
    </IfModule>


#### Maintenance page redirection

    # Redirect traffic

    RewriteEngine on
    RewriteCond %{REQUEST_URI} !/maintenance.html$
    RewriteCond %{REMOTE_ADDR} !¹²³\.123\.123\.123
    RewriteRule $ /maintenance.html [R=302,L]


#### Blocking cross-site scripting(XSS)

    <IfModule mod_rewrite.c>
    RewriteCond %{QUERY_STRING} (\|%3E) [NC,OR]
    RewriteCond %{QUERY_STRING} GLOBALS(=|\[|\%[0–9A-Z]{0,2}) [OR]
    RewriteCond %{QUERY_STRING} _REQUEST(=|\[|\%[0–9A-Z]{0,2})
    RewriteRule .* index.php [F,L]
    </IfModule>