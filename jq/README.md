The minimum images (< 5 MB) for running `jq` via Docker. It supports:

- `okapies/jq:1.5`
- `okapies/jq:1.6`

`jq` is a software invented by Stephen Dolan and distributed under MIT License. See https://github.com/stedolan/jq/blob/master/COPYING.

It is not useful, of course, where the Internet connectivity is limited or unstable. I recommend you to try installing `jq` to your environment directly at first.

## Usage
```
function jq() {
    docker run -i --rm okapies/jq:1.5 "$@"
}

$ jq --version
$ echo '{"foo": "hello, world"}' | jq .foo
"hello, world"
```
