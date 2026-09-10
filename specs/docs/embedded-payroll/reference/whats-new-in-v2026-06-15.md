---
updatedAt: 2026-06-09T14:53:26.000Z
---

Fetch the complete documentation index at: https://docs.gusto.com/embedded-payroll/llms.txt. Use this file to discover all available pages before exploring further. Append .md to any documentation page URL to get its markdown version.

# What's new in v2026-06-15

See our [Version upgrade guide](https://docs.gusto.com/embedded-payroll/docs/version-upgrade-guide#v2026-06-15) for more details on upgrading to v2026-06-15, which contains the following changes:

* Deprecated legacy terms of service endpoints in favor of new RESTful endpoints
  * Accept terms of service
    * **Deprecated**: [Accept terms of service for an admin](https://docs.gusto.com/embedded-payroll/reference/post-partner-managed-companies-company_uuid-accept_terms_of_service)
    * **Replacement**: [Accept the terms of service](https://docs.gusto.com/embedded-payroll/reference/post-v1-partner-managed-companies-company-uuid-terms_of_service)
  * Retrieve terms of service
    * **Deprecated**: [Retrieve terms of service status for an admin](https://docs.gusto.com/embedded-payroll/reference/post-partner-managed-companies-company_uuid-retrieve_terms_of_service)
    * **Replacement**: [Check the terms of service status for a user](https://docs.gusto.com/embedded-payroll/reference/put-v1-partner-managed-companies-company-uuid-terms_of_service)
* `GET /v1/companies/{company_id}/payrolls` now paginates by default when no pagination parameters are provided
  * Affected `Payroll` endpoint:
    * [Get all payrolls for a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-payrolls)
* Payroll receipt now returns paginated `employee_compensations`
  * Affected `Payroll` endpoint:
    * [Get a payroll receipt](https://docs.gusto.com/embedded-payroll/reference/get-v1-payment-receipts-payrolls-payroll_uuid)
* Off-cycle payroll creation now requires at least one `employee_uuid` in the request body. Requests without `employee_uuids`, with `null`, or with `[]` return 422. Termination payrolls (`off_cycle_reason: Dismissed employee`) retain the existing "exactly one employee" requirement.
  * Affected `Payroll` endpoint:
    * [Create an off-cycle payroll](https://docs.gusto.com/embedded-payroll/reference/post-v1-companies-company_id-payrolls)
* `payroll_status_meta.initial_check_date` and `payroll_status_meta.payroll_late` now return `null` for off-cycle payrolls. Previously these fields returned values that were not meaningful for off-cycle payrolls.
  * Affected `Payroll` endpoints:
    * [Get all payrolls for a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-payrolls)
    * [Get a single payroll](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-payrolls-payroll_id)
    * [Update a payroll](https://docs.gusto.com/embedded-payroll/reference/put-v1-companies-company_id-payrolls)
    * [Prepare a payroll](https://docs.gusto.com/embedded-payroll/reference/put-v1-companies-company_id-payrolls-payroll_id-prepare)
    * [Create an off-cycle payroll](https://docs.gusto.com/embedded-payroll/reference/post-v1-companies-company_id-payrolls)
* Employee compensation currency fields now return strings (e.g., `"1234.56"`) instead of floats.
  * Affected fields: `gross_pay`, `net_pay`, `check_amount`, `employee_deduction` (in benefits), `company_contribution` (in benefits), `amount` (in deductions, taxes, and hourly compensations), `qualified_earning_amount` (in qualified earnings)
  * Affected `Payroll` endpoints:
    * [Get all payrolls for a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-payrolls)
    * [Get a single payroll](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_id-payrolls-payroll_id)
    * [Update a payroll](https://docs.gusto.com/embedded-payroll/reference/put-v1-companies-company_id-payrolls)
    * [Prepare a payroll](https://docs.gusto.com/embedded-payroll/reference/put-v1-companies-company_id-payrolls-payroll_id-prepare)
    * [Calculate a payroll](https://docs.gusto.com/embedded-payroll/reference/put-v1-companies-company_id-payrolls-payroll_id-calculate)
* Removed the `setup_complete` field from the tax requirements response. Use `ready_to_run_payroll` instead.
  * Affected `Tax Requirements` endpoint:
    * [Get company tax requirements](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies-company_uuid-tax_requirements)
* New `uuid` fields included in compensation response objects (`hourly_compensations`, `fixed_compensations`, `paid_time_off`)
  * Affected `Company` endpoint:
    * [Get a company](https://docs.gusto.com/embedded-payroll/reference/get-v1-companies)
