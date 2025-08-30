# Red Hat Ansible Automation Platform - Network Tool Kit

This is an Ansible Content Collection focused on the network automation domain.  It contains roles and playbooks to help people quickly adopt some network automation use-cases with Ansible Automation Platform.

## Install

You can install this Ansible content with ansible-galaxy

```
ansible-galaxy collection install network.toolkit
```

## Network Report Configuration

### Customer Branding Variables

The `build_report_container` role supports customer branding customization. Configure these variables in `roles/build_report_container/vars/main.yml`:

```yaml
# Customer branding configuration
customer_name: "MOI"                    # Short name displayed in header
customer_full_name: "Ministry of Interior"  # Full name displayed as subtitle
customer_logo: "moi_Logo.png"          # Logo filename
show_customer_branding: true           # Enable/disable branding
show_customer_logo: true              # Enable/disable logo display
```

**To add your customer logo:**
1. Place your logo file in `roles/build_report_container/files/`
2. Update the `customer_logo` variable with your logo filename
3. Ensure `show_customer_logo: true` is set

### Report View Selection (Card vs List View)

The system supports two view modes for the report archive homepage:
- **Card View**: Grid layout with report cards (default)
- **List View**: Table layout with sortable rows

#### Quick Setup in Ansible Automation Platform

1. **Navigate to your Job Template** (e.g., "Network-Report")

2. **Enable Survey** - Toggle the "Survey Enabled" switch to ON

3. **Add Survey Question** - Click "Add" and configure:
   - **Question**: Select Report View Type
   - **Description**: Choose how reports should be displayed on the homepage
   - **Answer Variable Name**: `report_view_type`
   - **Answer Type**: Multiple Choice (single select)
   - **Multiple Choice Options**:
     ```
     Card View
     List View
     ```
   - **Default Answer**: Card View
   - **Required**: Yes

4. **Save** the survey and job template

#### Using Without Survey

You can also set the view type via extra variables:

```yaml
# In AAP Job Template - Extra Variables field:
report_view_type: "List View"

# Or via command line:
ansible-playbook playbooks/network_report.yml -e "report_view_type='List View'"
```

### Variable Precedence

The role checks for variables in this order:
1. Survey input / Extra variables
2. Role variables (`roles/build_report_container/vars/main.yml`)
3. Default values in tasks

## Ansible Network Automation Workshop

This Ansible Network Collection is used in conjunction with the Ansible Network Automation Workshop.  The workshops are instructor-led exercises to teach Ansible Automation.

Please refer to following links for more information and prescriptive exercises:
- The Workshops Landing Page - [https://ansible.github.io/workshops](https://ansible.github.io/workshops)
- The Github Source - [https://www.github.com/ansible/workshops](https://www.github.com/ansible/workshops)

## Network Roles

- [network.toolkit.backup](roles/backup/README.md)
- [network.toolkit.banner](roles/banner/README.md)
- [network.toolkit.build_report](roles/build_report/README.md)
- [network.toolkit.build_report_container](roles/build_report_container/README.md)
- [network.toolkit.facts](roles/facts/README.md)
- [network.toolkit.l3_interface](roles/l3_interface/README.md)
- [network.toolkit.reload](roles/reload/README.md)
- [network.toolkit.restore](roles/restore/README.md)
- [network.toolkit.system](roles/system/README.md)
- [network.toolkit.user](roles/user/README.md)

## Features

### Network Report System
- **Multi-view Support**: Toggle between Card and List views for report archive
- **Customer Branding**: Customizable headers and logos
- **AAP Integration**: Full support for Red Hat Ansible Automation Platform
- **Historical Archive**: Maintains all previous reports with metadata
- **Search & Filter**: Quick search across all report attributes
- **Containerized Deployment**: Uses Podman/Docker for web server

## Requirements

- Red Hat Ansible Automation Platform 2.x or AWX
- Podman or Docker installed on execution node
- Network devices accessible via SSH/NETCONF
- SELinux configured (handled automatically by role)

# License

[GNU General Public License v3.0 or later](LICENSE)
