#FUFF


Based on the information in the Network tab, we know we need to send a POST request to http://enum-sandbox/auth/login and how to structure the POST body.

Let's run ffuf. We'll set our wordlist with -w users.txt, specify our target URL with -u, use -X POST to send a POST request, set our POST body with -d, and specify our Content-Type header with -H. When we enter our POST body, we'll add "FUZZ" to the location we want ffuf to fuzz.

ffuf -w users.txt -u http://enum-sandbox/auth/login -X POST -d 'username=FUZZ&password=bar' -H 'Content-Type: application/x-www-form-urlencoded'

Since we didn't include any filter conditions, ffuf displays a result for each item in our wordlist. It lists the HTTP status code, response size, number of words and lines, and how long the application took to respond. We know the response for the "foo" value is not a valid login. The other responses match in size, words, and lines, which indicates these are all likely invalid usernames.

When we fuzz applications, we need to be aware of how much noise we're making from a network detection perspective and how we might impact the application. If our fuzzing requests are too fast or frequent, we might cause a denial of service (DOS). Similarly, fuzzing login forms with valid usernames and invalid passwords might cause the application to lock out accounts.
