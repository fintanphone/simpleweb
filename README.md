# Simple HTTPD Server Example

The Example consists of HTTPD server demo with demostration of URI handling :
    1. URI \hello for GET command returns "Hello World!" message
    2. URI \echo for POST command echoes back the POSTed message

* Open the project configuration menu (`idf.py menuconfig`) to configure Wi-Fi or Ethernet. See "Establishing Wi-Fi or Ethernet Connection" section in [examples/protocols/README.md](../../README.md) for more details.

Notes in addition to below:
       URI \stations with GET handler has been added.
       

Defined using code starting with : static const httpd_uri_t stations = {

When user opens 192.168.x.xxx/stations

The following GET handler will be invoked:
      static esp_err_t stations_get_handler(httpd_req_t *req)



* In order to test the HTTPD server persistent sockets demo :
    1. compile and burn the firmware `idf.py -p PORT flash`
    2. run `idf.py -p PORT monitor` and note down the IP assigned to your ESP module. The default port is 80
    3. test the example :
        * run the test script : "python scripts/client.py \<IP\> \<port\> \<MSG\>"
            * the provided test script first does a GET \hello and displays the response
            * the script does a POST to \echo with the user input \<MSG\> and displays the response
        * or use curl (asssuming IP is 192.168.43.130):
            1. "curl 192.168.43.130:80/hello"  - tests the GET "\hello" handler
            2. "curl -X POST --data-binary @anyfile 192.168.43.130:80/echo > tmpfile"
                * "anyfile" is the file being sent as request body and "tmpfile" is where the body of the response is saved
                * since the server echoes back the request body, the two files should be same, as can be confirmed using : "cmp anyfile tmpfile"
            3. "curl -X PUT -d "0" 192.168.43.130:80/ctrl" - disable /hello and /echo handlers
            4. "curl -X PUT -d "1" 192.168.43.130:80/ctrl" -  enable /hello and /echo handlers

See the README.md file in the upper level 'examples' directory for more information about examples.
