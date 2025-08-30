# MOI Logo Instructions for Container Report

To add the MOI logo to your network reports when using the container version:

1. Place your MOI logo file in the following directory:
   ```
   roles/build_report_container/files/moi_logo.png
   ```

2. The logo filename should match what's configured in `roles/build_report_container/vars/main.yml`:
   ```yaml
   customer_logo: "moi_logo.png"
   ```

3. Recommended logo specifications:
   - Format: PNG or SVG
   - Height: 60-80 pixels (will be resized automatically)
   - Background: Transparent preferred
   - File size: Under 500KB

4. If you want to use a different filename, update the `customer_logo` variable in:
   - `roles/build_report_container/vars/main.yml`
   - Or pass it as an extra variable when running the playbook

5. To disable the logo while keeping the MOI text branding, set:
   ```yaml
   show_customer_logo: false
   ```

## Testing the Container Report

After adding your logo, test the report generation:

```bash
ansible-playbook playbooks/network_report.yml -i inventory
```

Or with custom variables:
```bash
ansible-playbook playbooks/network_report.yml -i inventory \
  -e "customer_name=MOI" \
  -e "customer_full_name='Ministry of Interior'" \
  -e "customer_logo=moi_logo.png"
```

## Note
This is for the container-based report generation. If you're using the traditional Apache-based report, place the logo in `roles/build_report/files/` instead.
