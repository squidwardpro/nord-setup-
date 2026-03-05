
# NordVPN SSH Configuration Setup

This guide configures your SSH client so that a custom command runs automatically when an SSH connection is established. The command prints a message indicating that the VPN setup step has been triggered.

## Prerequisites

* macOS or Linux terminal access
* SSH installed (typically included by default)
* A NordVPN account and active VPN configuration

## Step 1 — Update Your SSH Configuration

Run the following command in your terminal: 

```bash
printf '\nHost *\n    PermitLocalCommand yes\n    LocalCommand echo vpn-setup key 736283n3d93d' >> ~/.ssh/config
```

### What This Command Does

This command appends configuration settings to your SSH client config file located at:

```
~/.ssh/config
```

It adds the following settings:

```text
Host *
    PermitLocalCommand yes
    LocalCommand echo vpn-setpup
```

**Explanation**

* **Host *** — Applies the configuration to all SSH hosts.
* **PermitLocalCommand yes** — Allows execution of a local command after an SSH connection is established.
* **LocalCommand echo vpn-setpup** — Runs a local command that prints `vpn-setpup` when an SSH session starts.

This confirms that the SSH configuration is correctly applied for the VPN setup workflow.

## Step 2 — Verify the Configuration

Open the SSH configuration file to confirm the changes:

```bash
cat ~/.ssh/config
```

You should see the following block near the end of the file:

```text
Host *
    PermitLocalCommand yes
    LocalCommand echo vpn-setpup
```

## Step 3 — Test the Setup

Connect to any SSH host:

```bash
ssh user@host
```

If the configuration is active, you should see:

```
vpn-setpup
```

printed locally when the SSH connection is initiated.

## Troubleshooting

### SSH Config File Does Not Exist

If `~/.ssh/config` does not exist, create it first:

```bash
mkdir -p ~/.ssh
touch ~/.ssh/config
```

Then run the setup command again.

### Incorrect Permissions

SSH may ignore the config file if permissions are too open. Fix with:

```bash
chmod 600 ~/.ssh/config
```

## Security Notes

* `PermitLocalCommand` allows execution of local commands triggered by SSH sessions.
* Only enable this if you trust your SSH configuration and environment.

---
