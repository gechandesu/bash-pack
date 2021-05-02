# Handy Bash scripts

## Installation

I recomend install scripts into the home directory. Place they into `~/.local/bin`. If you don't have it, create it:

```bash
mkdir -p ~/.local/bin
```

Give executing rights for scripts:

```bash
chmod +x <script_name>
```

Check your PATH variable:

```bash
echo $PATH
```

If you don't find `/home/your_username/.local/bin` run:

```bash
echo 'export PATH+=:$HOME/.local/bin' >> ~/.bashrc && source ~/.bashrc
```

Done. Run `<script_name> --help` for check.

---

## http

Python 3 http.server runner.

```
Run Python 3 builtin HTTP Server.

Usage:
    http [OPTIONS]... [ARGS]...

Options:
    --cgi, cgi      run as CGI Server.
    -f, f           run Firefox.
    --help, help    print this message and exit.

Optional arguments:
    HOST            host to bind. Default: 0.0.0.0
    PORT            port to bind. Default: 8000
    DIR             directory to serve. Default: cwd.

Also HOST:PORT syntax is allowed.
```

Examples:

```bash
# Run HTTP Server and open http://0.0.0.0:8000/ in Firefox
$ http f
# Run HTTP Server at 0.0.0.0:1234
$ http 1234
```

## prntl

Print log. Simple logging tool.

```
Print formatted log to STDOUT and log file.

Usage:
    prntl [OPTIONS]... [ARGUMENTS]...

Options:
    -o, --output        set log file name. Default: printl.log.
    -f, --log-format    set log format. Formatting options:
                            %time   time; see '--time-format'.
                            %log    log string.
                        Example: prntl -f 'mylog %time : %log'
    -t, --time-format   set time format; see 'date --help'
                        or 'man date' for details.
                        Example: prntl -t '%D %T'
    -c, --no-color      remove ANSI color codes from log string.
    -p, --no-print      don't print log to STDOUT.
    -h, --help          show this help message and exit.
```

Usage:

```bash
$ echo 'some log string' | prntl -o /dev/null -f 'BACKUP: %time : %log'
BACKUP: 03 Feb 2021 20:47:03 +0300 : some log string
```

## esc

```
Escape whitespaces and specail characters in string.
Uses 'printf %q'. Read more in 'man printf'.

Usage:
    esc [OPTIONS]... [ARGS]...

Options:
    -o, --opts      add end of the options sign (double dash). See
                    SHELL BUILTIN COMMANDS in 'man bash' for more info.
    -h, --help      print this message and exit.
```

Example:

```bash
$ echo 'my un$escaped \sstring --foo' | esc -o
-- my\ un\$escaped\ \\sstring\ --foo
```

## view

```
Print highlighted text to STDOUT.

Usage:
    view [OPTIONS..] [ARGUMENTS]...

Options:
    -l --less   send output to 'less -R'
    -n --lines  less, but shows line nums (less -RN).
    -h --help   show this help message and exit.
```

Script depends on **highlight** package ([link](http://www.andre-simon.de/)):

```bash
$ sudo apt install highlight
```

## rng

```
Expand ranges like "1-10" into a number series.

Usage:
    rng [OPTIONS]... [ARGUMENTS]...

Options:
    -d        digits delimiter. Default: '\n'.
    -l        lines delimiter. Default: '\n'.
    -D        Set same delimiters for digits and lines.
    --help    print this help message and exit.

Example:
   $ rng 1-4,7,9-12 -D ' '
   1 2 3 4 7 9 10 11 12
```
