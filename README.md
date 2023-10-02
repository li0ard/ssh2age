# ssh2age

Convert SSH ed25519 keys to [age](https://github.com/FiloSottile/age) keys. Just CLI for [ssh-to-age](https://github.com/Mic92/ssh-to-age).

## Usage

- Convert private key (without password)

```console
$ ssh2age -p -i $HOME/.ssh/id_ed25519 -o key.txt
$ cat key.txt
 AGE-SECRET-KEY-1K3VN4N03PTHJWSJSCCMQCN33RY5FSKQPJ4KRRTG3JMQUYE0TUSEQEDH6V8
```

- Convert private key (with password)

```console
$ ssh2age -p -i $HOME/.ssh/id_ed25519 -o key.txt
 Enter SSH key password:
$ cat key.txt
 AGE-SECRET-KEY-1K3VN4N03PTHJWSJSCCMQCN33RY5FSKQPJ4KRRTG3JMQUYE0TUSEQEDH6V8
```

- Convert public key

```console
$ ssh2age -i $HOME/.ssh/id_ed25519.pub -o pub-key.txt
$ cat pub-key.txt
age17044m9wgakla6pzftf4srtl3h5mcsr85jysgt5fg23zpnta8sfdqhzn452
```

ssh2age also supports multiple public keys at once seperated by newlines and ignores unless ssh keys that are not in the ed25519 format. This makes it suiteable in combination with `ssh-keyscan`:

```console
$ curl "https://github.com/orlp.keys" | ssh2age
...
age1m6tk99c7q84g5luktuwve9d7pjz5zdfq7gt7w2rugc9nyn38eamqykdkh9
age164qlju7r0wwvuxgwam328rrk732scce7ds3ktlg5pw57yx5qlywqusqup4
age167f44ulejhgwm4ttrlpwsj99yr2evhgx234gjp5gtccdxmsrju4qrxdz2p
skipped key: got ssh-rsa key type, but only ed25519 keys are supported
age1ar0g7u4fsqpmzlx9u4k9v2k9hyr8642jt5h5jdly3takm4jhcutsh62j7m
```