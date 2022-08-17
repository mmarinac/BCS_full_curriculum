# Ajax

https://www.youtube.com/watch?v=23KZJjUD5lc&&index=17&list=PLryb4nu66MZcb_LqLyWo-KuVEltlOZ7nc


[https://youtu.be/23KZJjUD5lc](https://youtu.be/23KZJjUD5lc)

----------

**AJAX** stands for Asynchronous JavaScript And XML. In a nutshell, it is the use of the XMLHttpRequest object to communicate with servers. It can send and receive information in various formats, including JSON, XML, HTML, and text files

We use ajax to make calls to an external API because the response from it will not be instant, it will be asynchronous.
All this means is that it will take some time for the API to give us the data we are requesting, so we set up a function (call back) which will be executed when the data is delivered.


    let url = 'www.some_url.com'
    $.getJSON(url, function (data) {
        if(data){
          //handle the data and do someting with it.
        }else{
        // data is not here so something went wrong in your request.
    }

Let’s now see a real example this example will fetch the location using your ip address although this may not be 100%  accurate.

    $.getJSON('http://ip-api.com/json', function(data) {
            console.log('it works', data)
    })

Please note that $.getJSON depends on jQuery and won’t work if you dont’ have the library imported/installed.

