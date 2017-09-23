# php-extension
Sample of PHP extension

## 1 - Download PHP code

http://php.net/downloads.php

I used the mirror and version: br2.php.net

## 2 - Extract it 

```
tar -xvf php-7.1.9.tar.gz
```

## Access 'ext' folder and start creating an extension called 'hello'

```
cd php-7.1.9/ext
./ext_skel --extname=hello
```

## Edit config.m4 

Uncomment line 16 to 18. It will looks like as follows:

```
PHP_ARG_ENABLE(hello, whether to enable hello support,
[  --enable-hello           Enable hello support])
```

Uncomment line 43. It will looks like:

```
AC_DEFINE(HAVE_HELLOLIB,1,[ ])
```

## Configure the extension

Go to the php-7.1.9/ext/hello and type

```
phpize
```

This will setup the configure scripts based on the config.m4 file directly in this directory. Then type:

```
./configure --enable-hello
```

To generate makefiles

## Add new PHP function

Add on line 74 of 'hello.c' file (the comment must remain):

```
/* {{{ proto string hello_world(string arg)
   Say Hello World to everyone */
PHP_FUNCTION(hello_world)
{
    RETURN_STRING("Hello world");
}
/* }}} */
```

Now modify line 155 to the following (this will register the hello_world function):

```
const zend_function_entry hello_functions[] = {
    PHP_FE(confirm_hello_compiled,  NULL)       /* For testing, remove later. */
    PHP_FE(hello_world, NULL)
    PHP_FE_END  /* Must be the last line in hello_functions[] */
};
```

Save the hello.c file

## Compile the function

Type this in the extension dir.

```
make
make test
```

