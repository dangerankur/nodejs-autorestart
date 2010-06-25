# What is node.js auto restart 
 
it is a way to watch all .js files if they have been changed and to restart nodejs
to allow easy development.

## How to use nodejs auto restart:
 
copy `autoexit.js` and `nodejs.sh` to `/var/www/``
add to your script:

### at top: 
    require.paths.unshift(__dirname); //make local paths accecible

### and at end:
    require('autoexit');


### also you might want to use: `try-catch` witch will make your appplicaiton not crush on errors


### example:

    require.paths.unshift(__dirname); //make local paths accecible
    
    var sys = require('sys'),
       http = require('http');
    http.createServer(function (req, res) {
    
      try
      {
    
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.end('Hello World\n');
      
      }
      catch(e)
      {
       sys.puts(e.stack);
      }
      
    }).listen(8124, "127.0.0.1");
    sys.puts('Server running at http://127.0.0.1:8124/');
    
    require('autoexit');


### to launch nodejs you type
    cd /var/www
    ./nodejs.sh

to make it work with upstart  
copy `nodejs.conf` to `/etc/init/``

### to use upstart you type :

    [command] + [init filename without conf extention]

    start nodejs 
    stop nodejs
    restrt nodejs

### when i start to develop connect to the server with ssh and run:

    stop nodejs
    cd /var/www
    ./nodejs.sh


Then I will start to see application output and errors on the screen
If I want to stop the server I press `Control + C`
and the script stops.

### what files to watch?
Modify autoexit.js for your needs to watch other folders and file types