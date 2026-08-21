# Data Manager API Audiences by Addingwell

A Google Tag Manager **Server-Side** tag template to add or remove audience members in your **Google Ads** and **Display & Video 360** Customer Lists (Customer Match) through Google's [Data Manager API](https://developers.google.com/data-manager/api) — the successor of the Google Ads Customer Match upload APIs.

## Features

- **Server-to-server audience building**: feed your Customer Lists from your CRM, CDP, or website events, without relying on browser tags.
- **Add or remove members**: a single tag handles both `ingest` and `remove` operations on your Customer Lists.
- **Multiple destinations in one request**: Google Ads and Display & Video 360 Customer Lists.
- **Automatic SHA-256 hashing** of user data — email, phone, first/last name — with normalization (already-hashed values are passed through), in `HEX` or `BASE64` encoding.
- **Batch mode**: send up to 10,000 audience members in a single request from a members array.
- **Consent Mode support**: request-level and per-member consent, read from the incoming event and normalized (`granted`/`denied`/`true`/`false` → `CONSENT_GRANTED`/`CONSENT_DENIED`).
- **Customer Match Terms of Service** status handling, read from the tag configuration or the incoming event.
- **Test mode** (`Validate Only`): validate requests without modifying your Customer Lists.

## Quick start

1. Authorize your service account on the destination: grant it access to your Google Ads account (or MCC) and/or your Display & Video 360 advertiser.
2. Download [`template.tpl`](https://github.com/addingwell/data-manager-api-audiences-tag/blob/master/template.tpl) and import it in your GTM Server container (**Templates → Tag templates → New → ⋮ → Import**).
3. Create a tag from the template, choose the **Customer List Action** (add/remove), fill in your destinations (Operating Customer ID, Customer ID, Customer List ID), and trigger it on your audience event.
4. Send your events to the GTM Server endpoint in Measurement Protocol (GA4) format:

```json
{
    "events": [{
        "name": "members_upload",
        "params": {
            "terms_of_service": true,
            "consent": { "ad_user_data": "granted", "ad_personalization": "granted" },
            "user_data": {
                "email_address": "john.doe@acme.com",
                "phone_number": "+33627362122",
                "address": {
                    "first_name": "John",
                    "last_name": "Doe",
                    "country": "FR",
                    "postal_code": "75001"
                }
            }
        }
    }]
}
```

To send several members at once, enable **Batch Mode** and provide a `members` array (max 10,000 entries) instead of a single `user_data` object.

5. Test with `Validate Only` set to `true`, then switch it to `false` in production.

## Documentation

Full step-by-step guides (authentication, Measurement Protocol client, field mapping, batch mode, testing with Postman):

- 🇬🇧 [Google Ads & DV360 audiences with Data Manager API](https://docs.addingwell.com/en/data-manager-api/audiences)
- 🇫🇷 [Audiences Google Ads & DV360 avec Data Manager API](https://docs.addingwell.com/fr/data-manager-api/audiences)

## Support

Open an [issue](../../issues) or contact [support@addingwell.com](mailto:support@addingwell.com).

---

Maintained by [Addingwell](https://www.addingwell.com).
