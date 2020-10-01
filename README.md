# snippets

- [js](./js/README.md)
- [shopify](./shopify/README.md)
- [liquid](./shopify/Liquid.md)

### Little tips

- global installed npm packages
```
npm list -g --depth=0

```

- local ip
```
ifconfig | grep 'inet 192'| awk '{ print $2}'
``


## MySql

```
# bin
/usr/local/opt/mysql@5.7/bin/mysql
```

```
show global variables like "%datadir%";
```

##### Range function
>[1, 2, 3, 4, 5]
 - python3
```python
list(range(1,6))
```
 - php
```php
range(1,5)
```
 - js
```
[...Array(5).keys()].splice(1)
```

## Nginx

- Location Directive

> Priority high => low

```
http {
    sever {
        location = /a {
          echo "=/a";
        }

        location ^~ /a {
          echo "^~ /a";
        }

        location ~ /\w {
          echo "/\w";
        }

        location / {
          echo ="/";
        }
    }
}
```

- Reverse Proxy

```
http {
    server {
        listen    80;
        server_name localhost;
        default_type   text/html;

        location /a {
            proxy_pass http://192.168.0.12:80;
        }

        location /b/ {
            proxy_pass http://192.168.0.12:81/;
        }
    }
}
```

/a/** => http://192.168.0.12:80/a/**;
/b/** => http://192.168.0.12:81/**;

- Load Balancer

```
 http {

    upstream_group1 {
        server 192.168.0.12:80;
        server 192.168.0.12:81;
    }
    //upstream_group1 {
    //  server 192.168.0.12:80 weight=10;
    //  server 192.168.0.12:81 weight=1;
    //}
    server {
        listen    80;
        server_name localhost;
        default_type   text/html;

        location / {
            echo "/";
        }

        location /a {
            proxy_pass http://group1/;
        }
    }
}
```

## Regex

- [regexr](https://regexr.com/)

### Basic

- `.` => Matches any character except line breaks.
- `^` => Begining of the string.
- `$` => End of the string.
- `[^]` => Negataed set.
- `[]{3, }` => Match between 3 to unlimited characters.
- `\d <=> [0-9]`, `\D <=> [^0-9]`, `\w <=> [a-zA-Z0-9_]` // (alphanumeric & underscore).
- `\s <=> [\r\n\t\v ]` => Matches any whitespace character (spaces, tabs, line breaks).
- `{0,1} <=> ?` => Match between 0 and 1 times.
- `{0, } <=> *` => Match between 0 to unlimited times.
- `{1, } <=> +` => Match between 1 to unlimited times.

### Group

- use group

```
`xx@gmail.com`.match(/^([a-zA-Z0-9]\w*)@gmail\.com$/)[1] // 'xx'
```

- rename group

```
`xx@gmail.com`.match(/^(?<first>[a-zA-Z0-9]\w*)@gmail\.com$/).groups.first // 'xx'
```

- reuse group in regex

```
^(\d\d)\1$    // match 1212
```

- reuse group with renamed

```
^(?<first>\d+)\k<first>$
```

- `(?=` Positive lookahead

```js
'foobar, foopoo'.replace(/foo(?=bar)/g, 'replaced'); // "replacedbar, foopoo"
```

- `(?!` Negative lookahead

```js
'foobar, foopoo'.replace(/foo(?!bar)/g, 'replaced'); // "foobar, replacedpoo"
```

- `(?<=` Positive lookbehiend

```js
'foobar, foopoo'.replace(/(?<=foo)bar/g, 'replaced'); // "fooreplaced, foopoo"
```

- `(?<!` Negative lookbehiend

```js
'foobar, foopoo'.replace(/(?<=foo)bar/g, 'replaced'); // "foobar, fooreplaced"
```

### Examples

- match email address
  `^[a-zA-Z0-9]\w*@gmail\.com$` => `xx@gmail.com`

- match float string and get fixed
  `'rgba(100,150,200,.72312332)'.replace(/(\.\d{2})[0-9]*/,"$1"); // rgba(100,150,200,.72)`

- match two separate part
  `'/api/xxxx/edit?uu=xxxx&id=1&type=&page='.replace(/\/api|edit.*/g, '') // /xxxx/`

## Shell

#### `node (eval):1: command not found: _node` zsh problem

- update omz `upgrade_oh_my_zsh`
- delete all caches `rm ~/.zcompdump*`

#### ssh in pi from mac without password

```
# from mac
scp pi_rsa.pub pi@0.0.0.000:/home/pi/.ssh

# in pi
cat pi_rsa.pub >> authorized_keys

scp -i {{keypath}} {{filename}} {{user}}@{{host}}:{{targetpath}}
```

## [Xpath](http://xpather.com/)

## [Figma](https://www.figma.com/file/GAMKg6zWYqYId04ICOHOPq/funny?node-id=1%3A2)

## MacOs

 - Install broken app
```
sudo xattr -r -d com.apple.quarantine /Applications/XXX.app
```
 - [Change](https://github.com/stuartcryan/custom-iterm-applescripts-for-alfred) Alfred default terminal to iterm2
