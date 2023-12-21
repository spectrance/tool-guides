---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.16.0
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

<!-- #region -->
# 1. Install Git Credential Manager

## Linux

### 1. Install

Download the latest [.deb package*](https://github.com/git-ecosystem/git-credential-manager/releases/latest)

```bash
sudo dpkg -i <path-to-package>
git-credential-manager configure
```

#### How to Uninstall

```bash
git-credential-manager unconfigure
sudo dpkg -r gcm
```

### 2. Set Default Credential Store

```bash
export GCM_CREDENTIAL_STORE=secretservice
```
<!-- #endregion -->



```python

```
