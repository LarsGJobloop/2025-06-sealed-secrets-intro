# Sealed Secrets

## Command

- Create a new public/private key pair

  ```sh
  age-keygen > keys.txt
  ```

### Override `keys.txt` location

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

## References

- [SOPS](https://github.com/getsops/sops)
- [Age](https://github.com/FiloSottile/age)
