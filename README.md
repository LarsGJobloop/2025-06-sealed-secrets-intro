# Sealed Secrets

## Command

- Create a new public/private key pair

  ```sh
  age-keygen > keys.txt
  ```

### Override `keys.txt` location ([standard locations](https://github.com/getsops/sops?tab=readme-ov-file#23encrypting-using-age))

Prefix `sops` commands with an environment variable:

```sh
SOPS_AGE_KEY_FILE="$(pwd)/keys.txt" sops decrypt --in-place api-tokens
```

- Encrypt files

  ```sh
  sops encrypt --in-place api-tokens
  ```

- Decrypt files

  ```sh
  sops decrypt --in-place api-tokens
  ```

- Execute a command with decrypted file as environment variables

  ```sh
  sops exec-env api-tokens 'bash'
  ```

## References

- [SOPS](https://github.com/getsops/sops)
- [Age](https://github.com/FiloSottile/age)
