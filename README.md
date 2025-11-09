# Progress from Playbook to Role

This role is a significant evolution from the original [winupdate.yml playbook](https://github.com/gregheffner/playbooks/blob/main/winupdate.yml):

- **From Playbook to Role:**
  - The original playbook was a single-use, static automation for Windows patching.
  - This role is reusable, modular, and can be shared or published on Ansible Galaxy.
- **Configurability:**
  - The playbook had hardcoded update categories and logic.
  - The role exposes variables for update categories, reboot behavior, fact gathering, and diff reporting, making it flexible for many environments.
- **Best Practices:**
  - The role follows Ansible Galaxy standards for structure, metadata, and documentation.
  - Unneeded local logging and non-portable tasks have been removed for compliance and portability.
- **Documentation & Testing:**
  - The role includes a professional README, usage examples, and variable documentation.
  - Molecule scenarios are provided for automated testing and CI.
- **Idempotency & Robustness:**
  - The role is designed to be idempotent and robust for monthly patching cycles, with safe defaults and clear override options.

This growth enables you to manage Windows patching at scale, with clarity, maintainability, and community standards.
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
| windows_patch_log_file     | *(removed)*                     | *(Logging to file removed for Galaxy best practices)* |
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
 Patch results and package differences will be logged to the specified log file *(removed for Galaxy best practices)*.

## Testing
Molecule scenarios are included for CI and local testing.
