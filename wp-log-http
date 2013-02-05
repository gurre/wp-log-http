<?php
/*
Plugin Name: http-logger
Description: Allows logging of all http-requests
Version: 0.0.1
Author: Gustav Svalander
Author URI: http://github.com/gurre/wp-log-http
*/

// Source: https://gist.github.com/hinnerk-a/2846011
function wp_log_http_requests( $response, $args, $url ) {
  // set your log file location here
	$logfile = plugin_dir_path( __FILE__ ).'/http.log';

	// parse request and response body to a hash for human readable log output
	$log_response = $response;
	if ( isset( $args['body'] ) ) {
		parse_str( $args['body'], $args['body_parsed'] );
	}
	if ( isset( $log_response['body'] ) ) {
		parse_str( $log_response['body'], $log_response['body_parsed'] );
	}
	// write into logfile
	file_put_contents( $logfile, sprintf("%s,%s,%s\n", date( 'c' ), $url, json_encode($args) ), FILE_APPEND );
	//file_put_contents($logfile, sprintf("%s,%s",print_r($log_response,true) ));
	return $response;
}

// hook into WP_Http::_dispatch_request()
add_filter( 'http_response', 'wp_log_http_requests', 10, 3 );

?>
