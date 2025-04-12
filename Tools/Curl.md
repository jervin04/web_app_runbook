# Curl

When using curl, we can use the -i or --include options to include response headers in the output. If we only want the headers, we can use -I or --head.
use curl with -I to get the server headers on port 80 of the enumeration sandbox.
curl -I http://enum-sandbox
