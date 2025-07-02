# Sealed Secrets

> [!WARNING]
> Be careful not to lock yourself out while securing your secrets.
> [A cautionary story](https://medium.com/@amanat361/shamir-secret-sharing-the-story-of-a-catastrophic-bug-and-the-resilience-of-paypal-2d6104778b77)

Manage encrypted configuration using [sops](https://github.com/getsops/sops) and [age](https://github.com/FiloSottile/age).

## References

- [sops](https://github.com/getsops/sops): Encrypt/decrypt files
- [age](https://github.com/FiloSottile/age): Modern encryption tool
  - [age-keygen](https://github.com/FiloSottile/age): Key pair generation

## Basic Workflow

- **Generate a new key pair**
  > [!IMPORTANT]
  > Store your `keys.txt` securely and never commit it to Git!
  
  ```sh
  age-keygen > keys.txt
  ```

  > If `keys.txt` isn’t in a [standard location](https://github.com/getsops/sops?tab=readme-ov-file#23encrypting-using-age), prefix commands:
  >
  > ```sh
  > SOPS_AGE_KEY_FILE="$(pwd)/keys.txt" sops decrypt --in-place my-secrets.yaml
  > ```

- **Encrypt a file**

  ```sh
  sops encrypt --in-place <file>
  ```

- **Decrypt a file**

  ```sh
  sops decrypt --in-place <file>
  ```

- **Run a command with decrypted content as environment variables**

  ```sh
  sops exec-env --pristine <file> 'bash'
  ```

  - Minimalistic example

    ```sh
    sops exec-env --pristine <file> 'bash -c "printenv; exit"'
    ```

- **Run a command with decrypted file as an argument**

  ```sh
  sops exec-file <file> 'echo "Filepath: {}"'
  ```

- **Update recipient keys**
  
  1. Decrypt with existing key
  2. Re-encrypt for new recipients

  ```sh
  sops updatekeys <file>
  ```

- **Rotate data encryption key**

  ```sh
  sops rotate <file>
  ```
