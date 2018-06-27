# Registering the key

You can use the keystore to generate a private key with a self signed certificate.

You can export the public key from the keystore in ssh format and send this to the party you want to communicate with.
If you are adding it to a server you control, you can simply copy the public key file there and add it to the authorized_keys file of the user you are logging in as:

```
$cat id_rsa_test-key.pub >> ~/.ssh/authorized_keys
```

Note that the public keys are generated with a trailing linefeed to enable this.

# Authentication

The sftp provider supports a number of query parameters:

- privateKey: the url of a private key
- password: the password for the private key
- publicKey: the url of the public key (optional, not required, the private key is enough)

You can set the username (and optionally the user password) in the URL:

```
sftp://myUser@localhost/path/to
sftp://myUser:myPass@localhost/path/to
```

Note that the credentials are stripped from the URI when displayed later on.

## SSH Keys from the keystore

You can use the privateKey url to point to the file system or a file you manually uploaded to the repository somewhere, e.g. ``repository:my.artifact:/private/my_key``

You can also get a privateKey from a keystore, you do not need to enter the password of the keystore nor the password that is set on the private key (if any), simply use: ``repository:my.keystore:/artifact/test-key:ssh-priv``.

Where "test-key" is the alias of the key and "ssh-priv" is the format. You can also use "ssh-pub" to read the ssh public key if necessary.

# Examples

```
sftp://alex@localhost/tmp/test.txt?privateKey=repository:test.keystore:/artifact/test-key:ssh-priv
```