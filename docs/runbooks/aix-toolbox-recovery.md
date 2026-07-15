# AIX Toolbox Recovery and DNF Migration

## Purpose

This document describes the process used to recover a legacy AIX Toolbox installation and migrate from a broken Yum environment to a functioning DNF environment.

This procedure was developed while recovering a production AIX 7.2 server and is intended to be reused on similar systems.

---

# Symptoms

Common symptoms include:

- `dnf` not found
- `dnf` loader errors
- `yum` loader errors
- `wget` loader errors
- Missing `libcrypto`
- Missing `libssl`
- Missing `libgcc`
- `Cannot run a file that does not have a valid format`
- GPG signature failures
- Broken package dependencies

---

# Prechecks

Capture the current system state before making any changes.

```sh
oslevel -s

rpm --version

lslpp -L rpm.rte

rpm -qa | sort
```

Verify package managers.

```sh
which yum
which dnf
which python3

yum --version
dnf --version
```

Record any loader errors.

---

# Validate OpenSSL

Verify both the AIX fileset and Toolbox RPM.

```sh
lslpp -L openssl.base

rpm -qi openssl
```

Inspect the libraries.

```sh
ls -l \
    /usr/lib/libcrypto.a \
    /usr/lib/libssl.a \
    /opt/freeware/lib/libcrypto.a \
    /opt/freeware/lib/libssl.a
```

Determine which package owns the Toolbox libraries.

```sh
rpm -qf /opt/freeware/lib/libcrypto.a
rpm -qf /opt/freeware/lib/libssl.a
```

---

# Validate GCC Runtime

Check the installed runtime.

```sh
rpm -q libgcc
rpm -q libstdc++
```

Older GCC 4.8 runtimes should be upgraded before attempting DNF recovery.

---

# DNF Runtime Architecture

One important lesson learned during recovery:

DNF uses the **32-bit** Python runtime.

Correct:

```text
/opt/freeware/libexec/python3.12_32
```

Not:

```text
/opt/freeware/bin/python3
```

Validate DNF using:

```sh
/opt/freeware/libexec/python3.12_32 \
    -c 'import dnf; print(dnf.__version__)'
```

---

# Common Problems

## Obsolete OpenSSL RPM

Symptoms:

```
libcrypto.so.3 not found
```

Cause:

An obsolete Toolbox OpenSSL package installed under:

```
/opt/freeware/lib
```

shadowed the AIX OpenSSL 3 libraries.

---

## Obsolete GCC Runtime

Symptoms:

```
Cannot run a file that does not have a valid format
```

Resolution:

Upgrade:

- libgcc8
- libstdc++8
- libgcc
- libstdc++

---

## Legacy Monitoring Software

Old Nagios packages depended upon the obsolete OpenSSL RPM.

Packages encountered:

- nagios-nrpe
- nagios-plugins

Always test removal first.

```sh
rpm -e --test \
    nagios-nrpe \
    nagios-plugins \
    openssl
```

---

## DNF GPG Failures

Some older IBM Toolbox packages remain unsigned.

Validate:

- Repository URLs
- RPM digests

If packages originate from IBM Toolbox repositories:

```sh
dnf install <package> --nogpgcheck
```

Use `--nogpgcheck` only for the affected transaction.

---

# Recovery Workflow

```text
Assess Environment
        ↓
Validate RPM
        ↓
Repair GCC Runtime
        ↓
Validate OpenSSL
        ↓
Remove obsolete OpenSSL RPM
        ↓
Remove obsolete Nagios packages
        ↓
Run updtvpkg
        ↓
Validate DNF
        ↓
Install current packages
        ↓
Post Validation
```

---

# Validation Checklist

```sh
dnf check

dnf repolist

git --version

which git

git status

rpm -qa | grep libgcc

rpm -qa | grep openssl
```

---

# Lessons Learned

- Always use `rpm -e --test` before removing packages.
- Validate before making changes.
- Loader errors usually indicate dependency problems rather than application failures.
- Verify 32-bit versus 64-bit executables before troubleshooting Python import errors.
- Modernize the runtime before reinstalling applications.
- Verify IBM repository URLs before using `--nogpgcheck`.
- `dnf check` is an excellent final health validation.
- Upgrade runtime libraries before application packages.
- Keep package changes grouped logically so they can be tested and rolled back if necessary.

---

# Future Improvements

- Create a `toolbox-doctor` utility.
- Create a `toolbox-report` inventory command.
- Automate the recovery workflow as an Ansible playbook.
- Standardize Toolbox validation across all AIX servers.
