## Qr Code App

Qr Code App

Print format QR generation code:

{% set total_taxes_and_charges = '%.2f' | format(doc.total_taxes_and_charges | float) %}
{% set grand_total = '%.2f' | format(doc.grand_total | float) %}
{% set posting_date = frappe.utils.get_datetime(doc.posting_date).strftime('%Y-%m-%d') %}
{%- set posting_time = frappe.utils.get_time(doc.posting_time).strftime('%H:%M:%S') -%}
{% set tax_id = '' %}
{% if frappe.db.get_value('Company', doc.company, 'tax_id') != None %}
    {% set tax_id = frappe.db.get_value('Company', doc.company, 'tax_id') %}
{% endif %}
{% set date_time = posting_date + 'T' + posting_time %}
{% set qr_code = [['1', doc.company], ['2', tax_id], ['3', date_time], ['4', grand_total], ['5', total_taxes_and_charges]] %}

QR Img Calling Jinja Tag:
{% if doc.docstatus == 1 and doc.ksa_einv_qr %}
  <div class="qrcode" style="width: 120px; text-align: left !important;"> {{ get_qr(qr_code)}} </div>
{% endif %}

#### License

mit
