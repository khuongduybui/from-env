# 🕶 from-env 🕶

from-env is helper script that makes environment variables from a local ``.env``-file inside command line statements available.

[![Gitpod Ready-to-Code](https://img.shields.io/badge/Gitpod-Ready--to--Code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/khuongduybui/from-env) 

## installation

```bash
npm install --save-dev from-env-with-command
```

## usage

``.env``
```.env
VARIABLE1=needs
VARIABLE2=have
VARIABLE3=variables
```

``expansions inside .env``
```.env
PORT=5000
PROTOCOL=http
HOST=localhost
URL=${PROTOCOL}://${HOST}:${PORT}
```

```package.json``` (before)
```json
{
    "scripts": {
        "yo": "your-command --that needs --to have --some variables"
    }
}
```

```package.json``` (after)
```json
{
    "scripts": {
        "yo": "from-env your-command --that %VARIABLE1 --to %VARIABLE2 --some %VARIABLE3"
    }
}
```

### embedded variables replacement

To enable replacing variables that are not standlone:

`from-env --embedded-vars your-command --things thing1=%VARIABLE1 thing2=%VARIABLE2 --other $VARIABLE3`

or

`from-env your-command --things thing1=%VARIABLE1 thing2=%VARIABLE2 --other $VARIABLE3`

with

``.env``
```.env
FROM_ENV_EMBEDDED=true
```

## alternative

this also works without any package (also on windows with wsl):

```package.json```
```json
{
    "scripts": {
        "yo": "from-env your-command --that $(grep VARIABLE1 .env | cut -d '=' -f2) --to $(grep VARIABLE2 .env | cut -d '=' -f2) --some $(grep VARIABLE3 .env | cut -d '=' -f2)"
    }
}
```
