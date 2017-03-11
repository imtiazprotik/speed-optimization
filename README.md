# Speed Up WordPress through .htaccess

	Header unset ETag  
	FileETag None
	 
	# BEGIN Expire headers  
	<ifModule mod_expires.c>  
	    ExpiresActive On  
	    ExpiresDefault "access plus 2592000 seconds"  
	    ExpiresByType image/x-icon "access plus 2592000 seconds"  
	    ExpiresByType image/jpeg "access plus 2592000 seconds"  
	    ExpiresByType image/png "access plus 2592000 seconds"  
	    ExpiresByType image/gif "access plus 2592000 seconds"  
	    ExpiresByType application/x-shockwave-flash "access plus 2592000 seconds"  
	    ExpiresByType text/css "access plus 604800 seconds"  
	    ExpiresByType text/javascript "access plus 216000 seconds"  
	    ExpiresByType application/javascript "access plus 216000 seconds"  
	    ExpiresByType application/x-javascript "access plus 216000 seconds"  
	    ExpiresByType application/xhtml+xml "access plus 600 seconds"
	    ExpiresByType text/html "access plus 1 day" 
	</ifModule>  
	# END Expire headers
	 
	# BEGIN Cache-Control Headers  
	<ifModule mod_headers.c>  
	    <filesMatch "\.(ico|jpe?g|png|gif|swf)$">  
	        Header set Cache-Control "public"  
	    </filesMatch>  
	    <filesMatch "\.(css)$">  
	        Header set Cache-Control "public"  
	    </filesMatch>  
	    <filesMatch "\.(js)$">  
	        Header set Cache-Control "private"  
	    </filesMatch>  
	    <filesMatch "\.(x?html?|php)$">  
	        Header set Cache-Control "private, must-revalidate"  
	    </filesMatch>  
	</ifModule>  
	# END Cache-Control Headers
	 
	# BEGIN GZIP (May not work on all servers)
	# mod_gzip compression (legacy, Apache 1.3)
	<IfModule mod_gzip.c>
	mod_gzip_on Yes
	mod_gzip_dechunk Yes
	mod_gzip_item_include file \.(html?|xml|txt|css|js)$
	mod_gzip_item_include handler ^cgi-script$
	mod_gzip_item_include mime ^text/.*
	mod_gzip_item_include mime ^application/x-javascript.*
	mod_gzip_item_exclude mime ^image/.*
	mod_gzip_item_exclude rspheader ^Content-Encoding:.*gzip.*
	</IfModule>
	# END GZIP
	 
	# DEFLATE compression
	<IfModule mod_deflate.c>
	# Set compression for: html,txt,xml,js,css
	AddOutputFilterByType DEFLATE text/html text/plain text/xml application/xml application/xhtml+xml text/javascript text/css application/x-javascript
	# Deactivate compression for buggy browsers
	BrowserMatch ^Mozilla/4 gzip-only-text/html
	BrowserMatch ^Mozilla/4.0[678] no-gzip
	BrowserMatch bMSIE !no-gzip !gzip-only-text/html
	# Set header information for proxies
	Header append Vary User-Agent
	</IfModule>
	# END DEFLATE

#BR cashing

	<IfModule mod_expires.c>

	    ExpiresActive on
	    ExpiresDefault                                      "access plus 1 month"

	  # CSS

	    ExpiresByType text/css                              "access plus 1 year"


	  # Data interchange

	    ExpiresByType application/atom+xml                  "access plus 1 hour"
	    ExpiresByType application/rdf+xml                   "access plus 1 hour"
	    ExpiresByType application/rss+xml                   "access plus 1 hour"

	    ExpiresByType application/json                      "access plus 0 seconds"
	    ExpiresByType application/ld+json                   "access plus 0 seconds"
	    ExpiresByType application/schema+json               "access plus 0 seconds"
	    ExpiresByType application/vnd.geo+json              "access plus 0 seconds"
	    ExpiresByType application/xml                       "access plus 0 seconds"
	    ExpiresByType text/xml                              "access plus 0 seconds"


	  # Favicon (cannot be renamed!) and cursor images

	    ExpiresByType image/vnd.microsoft.icon              "access plus 1 week"
	    ExpiresByType image/x-icon                          "access plus 1 week"

	  # HTML

	    ExpiresByType text/html                             "access plus 0 seconds"


	  # JavaScript

	    ExpiresByType application/javascript                "access plus 1 year"
	    ExpiresByType application/x-javascript              "access plus 1 year"
	    ExpiresByType text/javascript                       "access plus 1 year"


	  # Manifest files

	    ExpiresByType application/manifest+json             "access plus 1 week"
	    ExpiresByType application/x-web-app-manifest+json   "access plus 0 seconds"
	    ExpiresByType text/cache-manifest                   "access plus 0 seconds"


	  # Media files

	    ExpiresByType audio/ogg                             "access plus 1 month"
	    ExpiresByType image/bmp                             "access plus 1 month"
	    ExpiresByType image/gif                             "access plus 1 month"
	    ExpiresByType image/jpeg                            "access plus 1 month"
	    ExpiresByType image/png                             "access plus 1 month"
	    ExpiresByType image/svg+xml                         "access plus 1 month"
	    ExpiresByType image/webp                            "access plus 1 month"
	    ExpiresByType video/mp4                             "access plus 1 month"
	    ExpiresByType video/ogg                             "access plus 1 month"
	    ExpiresByType video/webm                            "access plus 1 month"


	  # Web fonts

	    # Embedded OpenType (EOT)
	    ExpiresByType application/vnd.ms-fontobject         "access plus 1 month"
	    ExpiresByType font/eot                              "access plus 1 month"

	    # OpenType
	    ExpiresByType font/opentype                         "access plus 1 month"

	    # TrueType
	    ExpiresByType application/x-font-ttf                "access plus 1 month"

	    # Web Open Font Format (WOFF) 1.0
	    ExpiresByType application/font-woff                 "access plus 1 month"
	    ExpiresByType application/x-font-woff               "access plus 1 month"
	    ExpiresByType font/woff                             "access plus 1 month"

	    # Web Open Font Format (WOFF) 2.0
	    ExpiresByType application/font-woff2                "access plus 1 month"


	  # Other

	    ExpiresByType text/x-cross-domain-policy            "access plus 1 week"

	</IfModule>