# Python-PHP-Package

This is a simple Python package that allows the client to interface with the system's PHP command without having to make lower level BASH commands or creating threads. This was a work in progress. Feel free to create a pull request to add more compataibility across operating systems.

It's important to keep in mind that this package *does not create* a PHP server. It only interfaces with the PHP that (hopefully) exists on the system.

# Usage
## Example
```python3
import php.server
import php.finder

php_location = php.finder.get_php_path()
php_server = PHPServer("path/to/files", "192.168.0.1:8888", php_location)
php_server.start()
# Some other code
php_server.stop()
```

## php.server
The `php.server` package provides the `PHPServer` object.
```  
PHPServer(dir, server_address, install_loc="php")
# dir is the base directory where the PHP files to be rendered are located
# server_address is the address with the form addrs:port 
# install_loc is the PHP executable location. By default, this argument calls "php" on the $PATH environment variable
```

The important methods it provides are the following
```
start()       # Start the server on a new thread
stop()        # Stop the server safely. It is strongly encouraged to always stop() the server after start()'ing it, else you run the risk of the server outliving the python code that started it.
kill()        # Stop the server unsafely. Unrecommended.
is_running()  # Returns true if the server is running.
```


## php.finder
The `php.finder` provides methods of searching for the PHP server executable. This is helpful if you're unsure whether the system has the PHP call in its #PATH environment variable.

It provides the following functions
```
get_php_path(allow_prompt=True) # Will attempt to find the PHP server executable location. If it is unable and allow_prompt is true, it will prompt the user through the console to supply it. This value is cached and a prompt won't be necessary again as long as the PHP server executable location doesn't move.
is_php_launcher(file_loc)  # Will check to see if file_loc is a true PHP server executable
save_path(file_loc)        # Overwrites the previously cached PHP server executable location
```

> This package was created for [Arachnid](https://github.com/jake-bickle/Arachnid) which has since matured and no longer needed it. Rather than delete the package, I hope that it would be of some use to someone else.
