# windows_desktop_patching

Ansible role to patch Windows desktops using Windows Update. Professional, configurable, and ready for production.

## Features
- Installs all available security, critical, and rollup updates (configurable)
- Optionally reboots if required (configurable)
- Logs patch results to a file (configurable)
- Optionally gathers facts and reports package differences before/after patching
- Idempotent and robust

## Role Variables

| Variable                   | Default                        | Description |
|----------------------------|--------------------------------|-------------|
| windows_patch_categories   | `[CriticalUpdates, SecurityUpdates, UpdateRollups]` | List of update categories to install |
| windows_patch_reboot       | `true`                         | Whether to reboot automatically after updates |
| windows_patch_log_file     | `C:\\patch_results.txt`        | Path to log file for patch results |
| windows_patch_gather_facts | `true`                         | Whether to gather facts before patching |
| windows_patch_report_diff  | `true`                         | Whether to compare and report package differences |

## Usage

Add this role to your playbook:

```yaml
- hosts: windows
  roles:
    - role: windows_desktop_patching
```

You can override any variable, for example:

```yaml
- hosts: windows
  vars:
    windows_patch_categories:
      - SecurityUpdates
    windows_patch_reboot: false
    windows_patch_log_file: C:\\custom_patch_log.txt
    windows_patch_gather_facts: false
    windows_patch_report_diff: false
  roles:
    - role: windows_desktop_patching
```

## Requirements
- Ansible 2.9+
- Windows hosts with WinRM enabled

## Example Output
Patch results and package differences will be logged to the specified log file. Use the debug output for package diff details.

## Testing
Molecule scenarios are included for CI and local testing.
