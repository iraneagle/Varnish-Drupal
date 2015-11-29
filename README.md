Varnish 4.X for Drupal 7.x

You need to use Drupal varnish-7.x-1.x-dev (Varnish 1.x-dev version compatible with Varnish 4.X)

As per the documentation on drupal.org/project/varnish you should add something like the following to your settings.php file:

/**
 * Add Varnish Caching.
 */
$conf['varnish_version'] = 4;

// Tell Drupal it's behind a proxy.
$conf['reverse_proxy'] = True;

// Tell Drupal what addresses the proxy server(s) use.
$conf['reverse_proxy_addresses'] = array('127.0.0.1');

// Bypass Drupal bootstrap for anonymous users so that Drupal sets max-age < 0.
$conf['page_cache_invoke_hooks'] = FALSE;

// Make sure that page cache is enabled.
$conf['cache'] = 1;
$conf['cache_lifetime'] = 0;
$conf['page_cache_maximum_age'] = 21600;

// Add Varnish as the page cache handler.
$conf['cache_backends'][] = 'projects/all/modules/varnish/varnish.cache.inc';
$conf['cache_class_cache_page'] = 'VarnishCache';
$conf['reverse_proxy_header'] = 'HTTP_X_FORWARDED_FOR';
$conf['omit_vary_cookie'] = False;
$conf['drupal_http_request_fails'] = FALSE;
