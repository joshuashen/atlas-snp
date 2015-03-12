ruby 1.9.0 is at least 5 times faster than 1.8.x in many cases. Here is the procedure to install it under your own home dir:

1. Download the source code from ruby-lang.org:

> `curl ftp://ftp.ruby-lang.org/pub/ruby/1.9/ruby-1.9.0-0.tar.gz > ruby-1.9.0-0.tar.gz`

and untar/gunzip it:

> `tar zxvf ruby-1.9.0-0.tar.gz`

2. Goto the directory ruby-1.9.0-0, then compile by typing these commands:

1) `./configure --prefix=/PATH/to/your_own_software_dir/`

/PATH/to/your\_own\_software\_dir/: For example, I used this dir on a linux server: /users/ys135495/opt/

2) `make`

Note: this step might be slow

3) `make install`

If no error occurred, you can use ruby-1.9.0 from /PATH/to/your\_own\_software\_dir/bin/ruby . In my case, it's /users/ys135495/opt/bin/ruby