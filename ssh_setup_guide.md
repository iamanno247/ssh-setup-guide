# Complete Guide: Setting Up SSH Keys for GitHub

This guide outlines the complete, step-by-step process for generating an SSH key pair, adding the public key to your GitHub account, and configuring your local repositories to use SSH authentication.

## Prerequisites

Ensure you have `git` and `ssh` tools available in your system terminal.

## Step 1: Generate a New SSH Key Pair

1. Open your terminal.

2. Run the following command (replace `your_email@example.com` with your GitHub email address):

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   > **Note:** `ed25519` is the modern, secure, and standard key format recommended by GitHub.

3. **File Location Prompt:** When prompted to *"Enter file in which to save the key,"* press `Enter` to accept the default location (`~/.ssh/id_ed25519`).

4. **Passphrase Prompt:** When prompted for a passphrase:

   * Press `Enter` twice to leave it empty (recommended for passwordless Git operations).

   * *Optionally*, enter a passphrase for extra key security.

## Step 2: Display and Copy the Public Key

You only share your **Public Key** (`id_ed25519.pub`). **Never share or expose your Private Key (`id_ed25519`).**

To view your public key on the terminal screen, run:

```bash
cat ~/.ssh/id_ed25519.pub
```

This will display your public key directly in your terminal window. Simply highlight the entire line with your mouse and copy it.

* **What to copy:** The entire output line starting with `ssh-ed25519` and ending with your email address (e.g., `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5... your_email@example.com`).

*(Optional: If you ever prefer copying directly to your clipboard without using the mouse, you can run `cat ~/.ssh/id_ed25519.pub | nix-shell -p xclip --run xclip` or `cat ~/.ssh/id_ed25519.pub | nix-shell -p wl-clipboard --run wl-copy` on NixOS).*

## Step 3: Add the SSH Key to GitHub

1. Log into your [GitHub Account](https://github.com).

2. Click your profile picture in the top-right corner and select **Settings**.

3. In the left sidebar under *Access*, click **SSH and GPG keys**.

4. Click the **New SSH key** (or **Add SSH key**) button.

5. In the **Title** field, give the key an identifiable label (e.g., `NixOS Laptop`, `Work PC`).

6. Set the **Key type** to **Authentication Key**.

7. In the **Key** field, paste the copied public key.

8. Click **Add SSH key**.

## Step 4: Test Your SSH Connection

Run the following command in your terminal to verify that GitHub recognizes your key:

```bash
ssh -T git@github.com
```

You should see a message similar to:

> *Hi username! You've successfully authenticated, but GitHub does not provide shell access.*

## Step 5: Switch Existing Repositories to SSH

If an existing Git project was cloned via HTTPS, switch its remote URL to use SSH:

1. Check your current remote URL:

   ```bash
   git remote -v
   ```

2. Update the remote URL to SSH format:

   ```bash
   git remote set-url origin git@github.com:USERNAME/REPOSITORY_NAME.git
   ```

3. Test pushing or pulling:

   ```bash
   git push
   ```

## Summary Checklist for New Machines

* [ ] Run `ssh-keygen -t ed25519 -C "email@example.com"`
* [ ] Display and copy key using `cat ~/.ssh/id_ed25519.pub`
* [ ] Add public key to GitHub under **Settings > SSH and GPG keys**
* [ ] Verify using `ssh -T git@github.com`
* [ ] Use `git@github.com:...` URLs when cloning or setting remote URLs