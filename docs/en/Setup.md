# Setup

To setup the module you'll need to create a private as well as an encryption key.

## Create private key

Ensure these keys are stored outside of your public web root.

```
openssl genrsa -out private.key 2048
openssl rsa -in private.key -pubout -out public.key
chmod 600 private.key
chmod 600 public.key
```

Add the private file path to your environment variables (ie. `.env`)
```
OAUTH_PRIVATE_KEY_PATH="/path/to/private.key"
OAUTH_PUBLIC_KEY_PATH="/path/to/private.key"
```

## Create Encryption Key

Generate a random key:

```
php -r 'echo base64_encode(random_bytes(32)), PHP_EOL;'
```

Add the encryption key your environment variables (ie. `.env`)

```
OAUTH_ENCRYPTION_KEY="<encryption key goes here>"
```

[Flows](Flows) &bullet; [Back to docs](Index.md)
