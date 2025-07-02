# Sealed Secrets

## Command

- Create a new public/private key pair

  ```sh
  age-keygen > keys.txt
  ```

> [!INFO]
> If you don't have the `keys.txt` in a standard location you can override it using:
> ```sh
> SOPS_AGE_KEY_FILE="$(pwd)/keys.txt" sops decrypt --in-place api-tokens
> ```

- Encrypt files

  ```sh
  sops encrypt --in-place api-tokens
  ```

- Decrypt files

  ```sh
  sops decrypt --in-place api-tokens
  ```

## References

- [SOPS]()
- [Age]()