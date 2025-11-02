# Installation Guide

## Step 1: Extract Archive

```bash
unzip gitdeb-package.zip
cd gitdeb-package
```

## Step 2: Install Script

```bash
sudo cp usr/local/bin/gitdeb /usr/local/bin/
sudo chmod +x /usr/local/bin/gitdeb
```

## Step 3: Copy Configuration

```bash
sudo cp -r etc/gitdeb /etc/
```

## Step 4: Initialize

```bash
sudo gitdeb init
```

## Step 5: Verify Installation

```bash
gitdeb version
gitdeb check
```

## Step 6: Install First Package

```bash
sudo gitdeb install vscode
```

## Step 7: Configure Auto-Updates (Optional)

```bash
sudo nano /etc/gitdeb/config.conf
```

Set:
```ini
AUTO_UPDATE_ENABLED="yes"
AUTO_UPDATE_INTERVAL="weekly"
AUTO_UPDATE_TIME="03:00"
```

Enable cron:
```bash
sudo gitdeb cron enable
```

## Step 8: Set Language (Optional)

```bash
sudo gitdeb set-language de
```

## Troubleshooting

### Missing Dependencies

```bash
sudo apt install curl jq dpkg apt gnupg
```

### Permission Issues

Make sure the script is executable:
```bash
sudo chmod +x /usr/local/bin/gitdeb
```

### GPG Key Issues

Import keys manually:
```bash
sudo gitdeb gpg-add 0xKEYID https://example.com/key.asc
```

### Check Logs

```bash
sudo tail -f /var/log/gitdeb.log
