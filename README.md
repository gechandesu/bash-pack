# Handy Bash scripts

## Installing

I recomend install scripts into the home directory. Place they into `~/.local/bin`. If you don't have it, create it:

```bash
mkdir -p ~/.local/bin
```

Give executing rights for scripts:

```bash
chmod +x <script_name>
```

Check your 'PATH' variable:

```bash
echo $PATH
```

If you don't find `/home/your_username/.local/bin` run:

```bash
echo 'export PATH=$PATH:$HOME/.local/bin' >> ~/.bashrc
source ~/.bashrc
```

All done. Run `<script_name> --help` for check.

---

## http

Python 3 http.server runner.

```
Run Python 3 HTTP Server.

Usage:
    http [OPTIONS]... [ARGS]...

Options:
    -c, --cgi       run HTTP Server as CGI Server.
    -l, --local     bind to localhost (default)
    -b, --bind      specify host to bind
    -d, --dir       specify directory to serve. CWD by default.
    -f, --firefox   run Firefox.
    -h, --help      print this message and exit.

Just run 'http' to serve current working directory at
http://localhost:8000/
Or 'http 1234' to run HTTP server on port 1234.

TODO:
dynamic port change if port is already in use by another process.
```

Examples:

```bash
# Run HTTP Server and open http://localhost:8000/ in Firefox
http -f
# Run HTTP Server at 0.0.0.0:1234
http -b 0.0.0.0:1234
```

## prntl

Print log. Simple logging tool.

```
prntl — print formatted log to STDOUT and log file.
Use '--no-print' option to write to log file only.

Usage: prntl [OPTION]... < [FILE]
Options:
    -o, --output        set log file. 'logfile' by default
    -f, --log-format    set log format. Formatting options:
                            %time   time; see --time-format
                            %log    log's string
                            Example: prntl -f 'mylog %time : %log'
    -t, --time-format   set time format; see 'date --help'
                        or 'man date' for details.
                        Example: prntl -t '%D %T'
    -c, --no-color      remove ANSI color codes from log string
    -p, --no-print      don't print log to STDOUT
    -h, --help          show this help message and exit.
```

Usage:

```bash
$ echo 'some log string' | prntl -o /dev/null -f 'BACKUP: %time : %log'
BACKUP: 03 Feb 2021 20:47:03 +0300 : some log string
```

## view

```
view — write highlighted text to STDOUT.
Options:
    	-l --less 	send output to less -R
    	-n --lines	less, but shows line nums (less -RN)
    	-h --help 	show this help message and exit.
```

Script depends on **highlight** package ([link](http://www.andre-simon.de/)):

```bash
sudo apt install highlight
```

## rng

```
rng - ranges expander.

This script expands expressions like "1-10" into a number series.
The resulting row can be used in conjunction with the xargs or
something else.

Example: rng 1-4,7,9-12
```

Use case:

```bash
$ rng 1-4,8,13 | xargs -I {} echo file_{}
file_1
file_2
file_3
file_4
file_8
file_13
```
