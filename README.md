# awskpass
`awskpass` is a bridge between [vaulted](https://github.com/miquella/vaulted) and [1Password](https://1password.com/) that makes it easy to unlock AWS environments without having to type a single character (outside of the command itself of course). Glad we left the dark ages of manual passwords behind, let's get started...

## Getting Started
1. Install and enable the 1Password CLI integration ([Get started with 1Password CLI](https://developer.1password.com/docs/cli/get-started/)).
2. Clone the repository somewhere on your machine.
    ```bash
    git clone https://github.com/bajankristof/awskpass.git ~/.awskpass
    ```
3. Add the `VAULTED_ASKPASS` environment to your bash profile (`~/.zshrc` for ZSH) with the path to the `awskpass` script.
    ```bash
    VAULTED_ASKPASS=~/.awskpass/awskpass
    ```
4. Add your vaulted profiles to `awskpass` (see below).
5. Enter a `vaulted shell` using your fingerprint / 1Password master password... Profit!

## Setting Up Profiles
For the script to work properly, you need to add your vaulted profiles to `awskpass` as well.

Profiles are just plain `.env` files within the `awskpass` installation directory.

Let's say you have a vaulted profile called `personal`. To make it work, you need to create a file named `personal.env` file inside the `awskpass` installation directory (in the above "default" directory this would be `~/.awskpass/personal.env`).

The file itself should contain something like this:
```bash
VAULTED_PASSWORD="op://Vault/xyz/vaulted password"
AWS_MFA_CODE="op://Vault/xyz/Section/one-time password?attribute=otp"
```

The values (secret references) can be copied from 1Password ([Get started with secret references](https://developer.1password.com/docs/cli/secret-references/)).

Here is an example of what a compatible 1Password entry would look like:
![1password-entry](https://github.com/bajankristof/awskpass/blob/main/screenshots/1password-entry.png "1password-entry")

(***NOTE:*** Generally speaking, you really only need the `one-time password` and the `vaulted password` fields, however I usually add the `vaulted password` field to my AWS entries so that they can be found in a single unified entry instead of being scattered across the vault.)
