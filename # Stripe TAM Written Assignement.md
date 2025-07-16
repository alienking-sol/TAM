# Stripe TAM Written Assignement

**Contents**

- Saving Customer Objects
- Auth and Capture
- Stripe Connect
- Responding to Users

## Question 1 | Saving Customer Objects

Using an API call, create a customer object leveraging a Visa test
payment method. Provide the customer object ID when this is complete.

**Customer Id:** cus_SgVtCz2hmBGNKK

**Payment Method Id:** pm_1Rl8rjB3KTBdesMMimQHvgT9


Documents referenced: https://docs.stripe.com/api/customers/create

```
stripe customers create --email="foster+TAM@gmail.com" --payment-method="pm_card_us"
```

Result

```json
{
  "id": "cus_SgVtCz2hmBGNKK",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1752585951,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "foster+TAM@gmail.com",
  "invoice_prefix": "YPV9ITIP",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": null,
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

I want to ensure the payment method for this customer is default too.

Documents referenced: https://docs.stripe.com/api/customers/update

```
stripe customers update cus_SgVtCz2hmBGNKK --invoice-settings.default-payment-method="pm_1Rl8rjB3KTBdesMMimQHvgT9"
```

Result

```json
{
  "id": "cus_SgVtCz2hmBGNKK",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1752585951,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "foster+TAM@gmail.com",
  "invoice_prefix": "YPV9ITIP",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": "pm_1Rl8rjB3KTBdesMMimQHvgT9",
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": null,
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

---

## Question 2 | Auth & Capture

### 2a. Use an API call to create an authorization for $100. Provide the Payment Intent ID related to this authorization.


**Payment Intent Id:** pi_3Rl9KAB3KTBdesMM0XTomcE8

Documents referenced: 
- https://docs.stripe.com/api/payment_intents/create
- https://docs.stripe.com/api/payment_intents/create?api-version=2025-06-30.preview#create_payment_intent-capture_method

Note: Use --capture-method="manual" so that only the authorization is made, not the completed charge

```
stripe payment_intents create --amount=10000 --currency="USD" --confirm=true --capture-method="manual" --customer="cus_SgVtCz2hmBGNKK" --payment-method="pm_1Rl8rjB3KTBdesMMimQHvgT9"
```

Result


``` json
{
  "id": "pi_3Rl9KAB3KTBdesMM0XTomcE8",
  "object": "payment_intent",
  "amount": 10000,
  "amount_capturable": 10000,
  "amount_details": {
    "tip": {}
  },
  "amount_received": 0,
  "application": null,
  "application_fee_amount": null,
  "automatic_payment_methods": {
    "allow_redirects": "never",
    "enabled": true
  },
  "canceled_at": null,
  "cancellation_reason": null,
  "capture_method": "manual",
  "charges": {
    "object": "list",
    "data": [
      {
        "id": "ch_3Rl9KAB3KTBdesMM0vtOak3k",
        "object": "charge",
        "amount": 10000,
        "amount_captured": 0,
        "amount_refunded": 0,
        "application": null,
        "application_fee": null,
        "application_fee_amount": null,
        "balance_transaction": null,
        "billing_details": {
          "address": {
            "city": null,
            "country": null,
            "line1": null,
            "line2": null,
            "postal_code": null,
            "state": null
          },
          "email": null,
          "name": null,
          "phone": null,
          "tax_id": null
        },
        "calculated_statement_descriptor": "Stripe",
        "captured": false,
        "created": 1752587714,
        "currency": "usd",
        "customer": "cus_SgVtCz2hmBGNKK",
        "description": null,
        "destination": null,
        "dispute": null,
        "disputed": false,
        "failure_balance_transaction": null,
        "failure_code": null,
        "failure_message": null,
        "fraud_details": {},
        "invoice": null,
        "livemode": false,
        "metadata": {},
        "on_behalf_of": null,
        "order": null,
        "outcome": {
          "advice_code": null,
          "network_advice_code": null,
          "network_decline_code": null,
          "network_status": "approved_by_network",
          "reason": null,
          "risk_level": "normal",
          "risk_score": 41,
          "seller_message": "Payment complete.",
          "type": "authorized"
        },
        "paid": true,
        "payment_intent": "pi_3Rl9KAB3KTBdesMM0XTomcE8",
        "payment_method": "pm_1Rl8rjB3KTBdesMMimQHvgT9",
        "payment_method_details": {
          "card": {
            "amount_authorized": 10000,
            "authorization_code": "524931",
            "brand": "visa",
            "capture_before": 1753192514,
            "checks": {
              "address_line1_check": null,
              "address_postal_code_check": null,
              "cvc_check": null
            },
            "country": "US",
            "exp_month": 7,
            "exp_year": 2026,
            "extended_authorization": {
              "status": "disabled"
            },
            "fingerprint": "eguNRKnG4W960IW0",
            "funding": "credit",
            "incremental_authorization": {
              "status": "unavailable"
            },
            "installments": null,
            "issuer": "Stripe Payments UK Limited",
            "last4": "4242",
            "mandate": null,
            "moto": null,
            "multicapture": {
              "status": "unavailable"
            },
            "network": "visa",
            "network_token": {
              "used": false
            },
            "network_transaction_id": "101103117788275",
            "overcapture": {
              "maximum_amount_capturable": 10000,
              "status": "unavailable"
            },
            "regulated_status": "unregulated",
            "three_d_secure": null,
            "wallet": null
          },
          "type": "card"
        },
        "radar_options": {},
        "receipt_email": null,
        "receipt_number": null,
        "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xUmprUVZCM0tUQmRlc01NKMO72cMGMgbxkvzewDg6LBZEyQoS1FvxKO4PBodyOTWpqDLsq2Rbo18Gf7zysDSlel827_ZVjPbFV3VC",
        "refunded": false,
        "review": null,
        "shipping": null,
        "source": null,
        "source_transfer": null,
        "statement_descriptor": null,
        "statement_descriptor_suffix": null,
        "status": "succeeded",
        "transfer_data": null,
        "transfer_group": null
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/charges?payment_intent=pi_3Rl9KAB3KTBdesMM0XTomcE8"
  },
  "client_secret": "pi_3R**********************_******_*********************BnRi",
  "confirmation_method": "automatic",
  "created": 1752587714,
  "currency": "usd",
  "customer": "cus_SgVtCz2hmBGNKK",
  "description": null,
  "invoice": null,
  "last_payment_error": null,
  "latest_charge": "ch_3Rl9KAB3KTBdesMM0vtOak3k",
  "livemode": false,
  "metadata": {},
  "next_action": null,
  "on_behalf_of": null,
  "payment_method": "pm_1Rl8rjB3KTBdesMMimQHvgT9",
  "payment_method_configuration_details": {
    "id": "pmc_1RjkR0B3KTBdesMMGbArMg9i",
    "parent": null
  },
  "payment_method_options": {
    "card": {
      "installments": null,
      "mandate_options": null,
      "network": null,
      "request_three_d_secure": "automatic"
    },
    "link": {
      "persistent_token": null
    }
  },
  "payment_method_types": [
    "card",
    "link"
  ],
  "processing": null,
  "receipt_email": null,
  "review": null,
  "setup_future_usage": null,
  "shipping": null,
  "source": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "requires_capture",
  "transfer_data": null,
  "transfer_group": null
}

```


---

### 2b. Log into your Stripe dashboard (https://dashboard.stripe.com/) and include a screenshot of the payment page for the authorization you just created.

![alt text](image.png)

### 2c. Use an API call to create a capture for $75.

Docs referenced: https://docs.stripe.com/api/payment_intents/capture?api-version=2025-06-30.preview

```
stripe payment_intents capture pi_3Rl9KAB3KTBdesMM0XTomcE8 --amount-to-capture=7500
```

```json
{
  "id": "pi_3Rl9KAB3KTBdesMM0XTomcE8",
  "object": "payment_intent",
  "amount": 10000,
  "amount_capturable": 0,
  "amount_details": {
    "tip": {}
  },
  "amount_received": 7500,
  "application": null,
  "application_fee_amount": null,
  "automatic_payment_methods": {
    "allow_redirects": "never",
    "enabled": true
  },
  "canceled_at": null,
  "cancellation_reason": null,
  "capture_method": "manual",
  "charges": {
    "object": "list",
    "data": [
      {
        "id": "ch_3Rl9KAB3KTBdesMM0vtOak3k",
        "object": "charge",
        "amount": 10000,
        "amount_captured": 7500,
        "amount_refunded": 0,
        "application": null,
        "application_fee": null,
        "application_fee_amount": null,
        "balance_transaction": "txn_3Rl9KAB3KTBdesMM07VpnlX1",
        "billing_details": {
          "address": {
            "city": null,
            "country": null,
            "line1": null,
            "line2": null,
            "postal_code": null,
            "state": null
          },
          "email": null,
          "name": null,
          "phone": null,
          "tax_id": null
        },
        "calculated_statement_descriptor": "Stripe",
        "captured": true,
        "created": 1752587714,
        "currency": "usd",
        "customer": "cus_SgVtCz2hmBGNKK",
        "description": null,
        "destination": null,
        "dispute": null,
        "disputed": false,
        "failure_balance_transaction": null,
        "failure_code": null,
        "failure_message": null,
        "fraud_details": {},
        "invoice": null,
        "livemode": false,
        "metadata": {},
        "on_behalf_of": null,
        "order": null,
        "outcome": {
          "advice_code": null,
          "network_advice_code": null,
          "network_decline_code": null,
          "network_status": "approved_by_network",
          "reason": null,
          "risk_level": "normal",
          "risk_score": 41,
          "seller_message": "Payment complete.",
          "type": "authorized"
        },
        "paid": true,
        "payment_intent": "pi_3Rl9KAB3KTBdesMM0XTomcE8",
        "payment_method": "pm_1Rl8rjB3KTBdesMMimQHvgT9",
        "payment_method_details": {
          "card": {
            "amount_authorized": 10000,
            "authorization_code": "524931",
            "brand": "visa",
            "capture_before": 1753192514,
            "checks": {
              "address_line1_check": null,
              "address_postal_code_check": null,
              "cvc_check": null
            },
            "country": "US",
            "exp_month": 7,
            "exp_year": 2026,
            "extended_authorization": {
              "status": "disabled"
            },
            "fingerprint": "eguNRKnG4W960IW0",
            "funding": "credit",
            "incremental_authorization": {
              "status": "unavailable"
            },
            "installments": null,
            "issuer": "Stripe Payments UK Limited",
            "last4": "4242",
            "mandate": null,
            "moto": null,
            "multicapture": {
              "status": "unavailable"
            },
            "network": "visa",
            "network_token": {
              "used": false
            },
            "network_transaction_id": "101103117788275",
            "overcapture": {
              "maximum_amount_capturable": 10000,
              "status": "unavailable"
            },
            "regulated_status": "unregulated",
            "three_d_secure": null,
            "wallet": null
          },
          "type": "card"
        },
        "radar_options": {},
        "receipt_email": null,
        "receipt_number": null,
        "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xUmprUVZCM0tUQmRlc01NKJDH2cMGMgYHOoXtqwo6LBazQwJ3lDswEk_nZ_B0-i3hvwz4gMH_3q7-LhsUGw-VwNlpm2LFvLmnBjfm",
        "refunded": false,
        "review": null,
        "shipping": null,
        "source": null,
        "source_transfer": null,
        "statement_descriptor": null,
        "statement_descriptor_suffix": null,
        "status": "succeeded",
        "transfer_data": null,
        "transfer_group": null
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/charges?payment_intent=pi_3Rl9KAB3KTBdesMM0XTomcE8"
  },
  "client_secret": "pi_3R**********************_******_*********************BnRi",
  "confirmation_method": "automatic",
  "created": 1752587714,
  "currency": "usd",
  "customer": "cus_SgVtCz2hmBGNKK",
  "description": null,
  "invoice": null,
  "last_payment_error": null,
  "latest_charge": "ch_3Rl9KAB3KTBdesMM0vtOak3k",
  "livemode": false,
  "metadata": {},
  "next_action": null,
  "on_behalf_of": null,
  "payment_method": "pm_1Rl8rjB3KTBdesMMimQHvgT9",
  "payment_method_configuration_details": {
    "id": "pmc_1RjkR0B3KTBdesMMGbArMg9i",
    "parent": null
  },
  "payment_method_options": {
    "card": {
      "installments": null,
      "mandate_options": null,
      "network": null,
      "request_three_d_secure": "automatic"
    },
    "link": {
      "persistent_token": null
    }
  },
  "payment_method_types": [
    "card",
    "link"
  ],
  "processing": null,
  "receipt_email": null,
  "review": null,
  "setup_future_usage": null,
  "shipping": null,
  "source": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```
---

### What happens to a charge if you only capture for a portion of an authorization, and not the full amount?

The $25 is released back to the same payment method of the customer. A partial capture will always release the remaining amount. If an authorization expires before capture, the funds are automatically released, and the payment status changes to canceled.

Docs referenced: https://docs.stripe.com/payments/place-a-hold-on-a-payment-method

![](2025-07-15-10-26-32.png)


### 2d. How do steps 2a-2c show on the customer’s bank statement?

Docs reference: https://docs.stripe.com/payments/place-a-hold-on-a-payment-method#:~:text=A%20partial%20capture%20automatically%20releases%20the%20remaining%20amount.

The pending authorization may remain visible for a short period even after the capture:

| Date           | Description | Status    | Amount |
| -------------- | ----------- | --------- | ------ |
| Feb 14th, 2024 | Amazon-123  | Pending   | - $100 |

Once the $75 charge is finalized, it would update in the ledger:

| Date           | Description | Status  | Amount |
| -------------- | ----------- | ------- | ------ |
| Feb 14th, 2024 | Amazon-123  | Confirmed | - $75 |


The remaining $25 is never actually charged and is simply released, it would just become available again in the customer’s account again

---


### 2e. Name and describe 2 distinct business models/use cases that would require auth and then capture at a later time.

### **Food Delivery App**

**How It Works**
- User places an order on an app  
- Merchant authorizes payment at checkout to ensure funds are available on the card  
- Funds are captured only when:  
  - The card’s available funds are confirmed, or  
  - The restaurant confirms the dish is in stock  

**Why This Model?**
- Prevents users from receiving food without having enough money  
- Protects restaurant owners from lost revenue due to failed payments or out-of-stock items  

### **Car Rental Service**

**How It Works**
- Traveller rents a car for a trip (ex. Toronto → Ottawa is 401 kms)  
- Rental company authorizes a capped amount (e.g., $1000) on the card at pick-up  
- Funds are captured only after:  
  - The car is returned and total kilometers are confirmed  
  - The final amount is calculated based on actual distance traveled  

**Why This Model?**
- Protects travellers from being overcharged for KMs they didn’t actually drive  
- Offers a flexible, usage-based payment experience instead of a flat rate (i.e. better CX)  


---

## Question 3 | Stripe Connect

For this question, you will be making API calls with Custom Connect accounts. Use this
[Connect test data](https://docs.stripe.com/connect/testing) as needed.

### 3a. Create a Custom Connect connected account. Provide the account ID.

Docs referenced:
- https://docs.stripe.com/connect/custom-accounts
- https://docs.stripe.com/connect/testing
- https://docs.stripe.com/connect/account-capabilities

**Account Id:** acct_1RlAGqPnLlHhkn0m
  
Notes:
- I will need to accept payments with this Connect Account, so I will need to enable some [capabilities](https://docs.stripe.com/connect/account-capabilities) for accepting card payments. 
- In order to enable account capabilities, I also need to [provide KYC info](https://docs.stripe.com/connect/handling-api-verification#:~:text=Connect%20platforms%20that%20onboard%20connected%20accounts%20using%20the%20API%20must%20provide%20Stripe%20with%20required%20information%20for%20Know%20Your%20Customer%20(KYC)%20purposes%20and%20to%20enable%20account%20capabilities). 


```
stripe accounts create --country="US" --capabilities.transfers.requested=true --business-type="individual" --individual.address.city="New York City" --individual.address.country="US" --individual.address.line1="address_full_match" --individual.address.postal-code="12345" --individual.address.state="NY" --individual.first-name="Adam" --individual.last-name="Driver" --individual.dob.day=1 --individual.dob.month=1 --individual.dob.year=1901 --default-currency="USD" --email="connect+test@gmail.com" --tos-acceptance.date=1752512515 --tos-acceptance.ip="140.54.99.164" --business-profile.url="https://accessible.stripe.com" --settings.card-payments.statement-descriptor-prefix="Driving" --type="custom"
```

Results
```json
{
  "id": "acct_1RlAGqPnLlHhkn0m",
  "object": "account",
  "activity": {
    "status": "active"
  },
  "business_profile": {
    "annual_revenue": null,
    "customer_regions": null,
    "estimated_worker_count": null,
    "funding_source": null,
    "mcc": null,
    "minority_owned_business_designation": null,
    "name": null,
    "product_description": null,
    "support_address": null,
    "support_email": null,
    "support_phone": null,
    "support_url": null,
    "url": "https://accessible.stripe.com"
  },
  "business_type": "individual",
  "can_generate_remediation_link": true,
  "can_unset_representative": false,
  "capabilities": {
    "transfers": "active"
  },
  "charges_enabled": true,
  "company": {
    "address": {
      "city": "New York City",
      "country": "US",
      "line1": "address_full_match",
      "line2": null,
      "postal_code": "12345",
      "state": "NY"
    },
    "directors_provided": true,
    "executives_provided": true,
    "name": null,
    "owners_provided": true,
    "tax_id_provided": false,
    "verification": {
      "details": null,
      "details_code": null,
      "document": {
        "back": null,
        "details": null,
        "details_code": null,
        "front": null
      },
      "status": "unverified"
    }
  },
  "compartment_id": "wksp_test_6SuYEC3JSQANe3Sfw6mpPtY",
  "connected_on": 1752591353,
  "controller": {
    "application": {
      "loss_liable": true,
      "onboarding_owner": true,
      "pricing_controls": true
    },
    "dashboard": {
      "type": "none"
    },
    "fees": {
      "payer": "application_custom"
    },
    "is_controller": true,
    "losses": {
      "payments": "application"
    },
    "requirement_collection": "application",
    "stripe_dashboard": {
      "type": "none"
    },
    "type": "application"
  },
  "controlling_platform": "acct_1RjkQVB3KTBdesMM",
  "controlling_platform_can_draw_funds": true,
  "controlling_platform_has_risk_controls": true,
  "controlling_platform_manages_capabilities": true,
  "country": "US",
  "created": 1752591353,
  "creation_request": "1752591351-req_hKQijdWckXuf2R",
  "dashboard_account_status": "restricted",
  "dashboard_type": "none",
  "default_account_holder_name": "ADAM DRIVER",
  "default_currency": "usd",
  "details_submitted": false,
  "email": "connect+test@gmail.com",
  "email_confirmed": false,
  "external_account_changes_disabled": false,
  "external_accounts": {
    "object": "list",
    "data": [],
    "has_more": false,
    "total_count": 0,
    "url": "/v1/accounts/acct_1RlAGqPnLlHhkn0m/external_accounts"
  },
  "fake_account": true,
  "future_requirements": {
    "alternatives": [],
    "current_deadline": null,
    "currently_due": [],
    "disabled_reason": null,
    "errors": [],
    "eventually_due": [],
    "past_due": [],
    "pending_verification": [],
    "previously_due": []
  },
  "individual": {
    "id": "person_1RlAGqPnLlHhkn0muFiCeK4r",
    "object": "person",
    "account": "acct_1RlAGqPnLlHhkn0m",
    "address": {
      "city": "New York City",
      "country": "US",
      "line1": "address_full_match",
      "line2": null,
      "postal_code": "12345",
      "state": "NY"
    },
    "created": 1752591352,
    "dob": {
      "day": 1,
      "month": 1,
      "year": 1901
    },
    "first_name": "Adam",
    "future_requirements": {
      "alternatives": [],
      "currently_due": [],
      "errors": [],
      "eventually_due": [],
      "past_due": [],
      "pending_verification": []
    },
    "id_number_country": "US",
    "id_number_keyed_in": false,
    "id_number_provided": false,
    "last_name": "Driver",
    "metadata": {},
    "personal_id_number_country": "US",
    "relationship": {
      "authorizer": false,
      "controller": false,
      "director": false,
      "executive": false,
      "legal_guardian": false,
      "officer": false,
      "owner": false,
      "partner": false,
      "percent_ownership": null,
      "representative": true,
      "title": null
    },
    "requirements": {
      "alternatives": [],
      "currently_due": [],
      "errors": [],
      "eventually_due": [
        "ssn_last_4"
      ],
      "past_due": [],
      "pending_verification": []
    },
    "ssn_last_4_provided": false,
    "verification": {
      "additional_document": {
        "back": null,
        "details": null,
        "details_code": null,
        "front": null
      },
      "details": null,
      "details_code": null,
      "document": {
        "back": null,
        "details": null,
        "details_code": null,
        "front": null
      },
      "status": "unverified"
    }
  },
  "invoice_settings": {
    "disable_legacy_credit_transfer_sources_types": true,
    "failure_days": 60,
    "hosted_payment_method_save_live": "offer",
    "hosted_payment_method_save_test": "offer",
    "invoicing_final_action": "none",
    "manual_tax_rounding_behavior": "group",
    "next_invoice_sequence_livemode": 1,
    "next_invoice_sequence_testmode": 1,
    "numbering_scheme": "customer_level",
    "pastdue_invoices_final_transition": "none",
    "pastdue_invoices_final_transition_days": 60,
    "payment_methods_enabled_for_merchant": {
      "ach_credit_transfer": false,
      "acss_debit": true,
      "affirm": false,
      "afterpay_clearpay": false,
      "alipay": false,
      "amazon_pay": true,
      "au_becs_debit": false,
      "bacs_debit": false,
      "bancontact": false,
      "boleto": false,
      "card": true,
      "cashapp": true,
      "crypto": true,
      "custom": false,
      "customer_balance": true,
      "demo_pay": false,
      "eps": false,
      "fpx": false,
      "giropay": false,
      "grabpay": false,
      "id_bank_transfer": false,
      "id_credit_transfer": false,
      "ideal": false,
      "jp_credit_transfer": false,
      "kakao_pay": true,
      "klarna": true,
      "konbini": false,
      "kr_card": true,
      "kr_market": false,
      "link": true,
      "multibanco": true,
      "naver_pay": true,
      "netbanking": false,
      "ng_bank_transfer": false,
      "ng_card": false,
      "ng_market": false,
      "ng_wallet": false,
      "nz_bank_account": false,
      "p24": false,
      "paper_check": false,
      "pay_by_bank": true,
      "payco": true,
      "paynow": false,
      "paypal": false,
      "promptpay": false,
      "revolut_pay": true,
      "samsung_pay": true,
      "sepa_credit_transfer": false,
      "sepa_debit": false,
      "sofort": false,
      "stripe_balance": false,
      "swish": false,
      "upi": false,
      "us_bank_account": true,
      "wechat_pay": true
    },
    "send_hosted_payment_email": true,
    "send_invoices": true,
    "smart_dunning_enabled": true,
    "supported_payment_methods": {
      "ach_credit_transfer": false,
      "acss_debit": false,
      "affirm": false,
      "afterpay_clearpay": false,
      "alipay": false,
      "amazon_pay": false,
      "au_becs_debit": false,
      "bacs_debit": false,
      "bancontact": false,
      "boleto": false,
      "card": true,
      "cashapp": true,
      "crypto": false,
      "custom": false,
      "customer_balance": true,
      "demo_pay": false,
      "eps": false,
      "fpx": false,
      "giropay": false,
      "grabpay": false,
      "id_bank_transfer": false,
      "id_credit_transfer": false,
      "ideal": false,
      "jp_credit_transfer": false,
      "kakao_pay": false,
      "klarna": false,
      "konbini": false,
      "kr_card": false,
      "kr_market": false,
      "link": true,
      "multibanco": false,
      "naver_pay": false,
      "netbanking": false,
      "ng_bank_transfer": false,
      "ng_card": false,
      "ng_market": false,
      "ng_wallet": false,
      "nz_bank_account": false,
      "p24": false,
      "paper_check": false,
      "pay_by_bank": false,
      "payco": false,
      "paynow": false,
      "paypal": false,
      "promptpay": false,
      "revolut_pay": false,
      "samsung_pay": false,
      "sepa_credit_transfer": false,
      "sepa_debit": false,
      "sofort": false,
      "stripe_balance": false,
      "swish": false,
      "upi": false,
      "us_bank_account": true,
      "wechat_pay": true
    }
  },
  "is_connected_v2_account": false,
  "legal_entity_shared_with": [],
  "merchants_reonboarded_to": [],
  "metadata": {},
  "nickname": "accessible.stripe",
  "payouts_enabled": false,
  "platform_can_request_capabilities": true,
  "platform_can_unrequest_capabilities": true,
  "primary_user": {
    "id": "usr_SgXLH4rNA94TsW",
    "object": "user",
    "email": null,
    "name": null,
    "password_set": null
  },
  "proration_settings": {
    "smart_prorations": false
  },
  "reonboarding_destination_merchants": [],
  "requirements": {
    "alternatives": [],
    "current_deadline": null,
    "currently_due": [
      "external_account"
    ],
    "disabled_reason": "requirements.past_due",
    "errors": [],
    "eventually_due": [
      "external_account",
      "individual.ssn_last_4"
    ],
    "past_due": [
      "external_account"
    ],
    "pending_verification": [],
    "previously_due": [
      "business_profile.url",
      "business_type",
      "individual.dob.day",
      "individual.dob.month",
      "individual.dob.year",
      "individual.first_name",
      "individual.last_name",
      "tos_acceptance.date",
      "tos_acceptance.ip"
    ]
  },
  "risk_controls": {
    "charges": {
      "pause_requested": false
    },
    "payouts": {
      "pause_requested": false
    }
  },
  "settings": {
    "bacs_debit_payments": {
      "display_name": null,
      "service_user_number": null
    },
    "branding": {
      "icon": null,
      "logo": null,
      "primary_color": null,
      "secondary_color": null,
      "show_support_phone": true
    },
    "card_issuing": {
      "tos_acceptance": {
        "date": null,
        "ip": null
      },
      "tos_acceptances": {
        "account_holder": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/ssa#services-terms"
        },
        "apple_pay_celtic": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/celtic/apple-payment-platform-program-manager-customer-terms-and-conditions#exhibit-c-pass-through-provisions"
        },
        "apple_pay_cross_river": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/crb/apple-payment-platform-program-manager-customer-terms-and-conditions#exhibit-c-pass-through-provisions"
        },
        "apple_pay_fifth_third": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/fifth-third/apple-payment-platform-program-manager-customer-terms-and-conditions#exhibit-c-pass-through-provisions"
        },
        "charge_card_celtic": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/celtic-charge-card"
        },
        "charge_card_celtic_platform": {
          "date": null,
          "ip": null,
          "url": null
        },
        "charge_card_cross_river": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/crb-charge-card"
        },
        "charge_card_cross_river_financing_disclosures": {
          "date": null,
          "ip": null,
          "url": null
        },
        "charge_card_cross_river_platform": {
          "date": null,
          "ip": null,
          "url": null
        },
        "charge_card_fifth_third": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/fifth-third-charge-card"
        },
        "charge_card_fifth_third_financing_disclosures": {
          "date": null,
          "ip": null,
          "url": null
        },
        "charge_card_fifth_third_platform": {
          "date": null,
          "ip": null,
          "url": null
        },
        "spend_card_celtic": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/celtic-spend-card"
        },
        "spend_card_cross_river": {
          "date": null,
          "ip": null,
          "url": "https://stripe.com/legal/issuing/crb-spend-card"
        },
        "spend_card_cross_river_financing_disclosures": {
          "date": null,
          "ip": null,
          "url": null
        }
      }
    },
    "card_issuing_payout": {
      "tos_acceptance": {
        "date": null,
        "ip": null
      }
    },
    "card_payments": {
      "decline_on": {
        "avs_failure": false,
        "cvc_failure": false
      },
      "statement_descriptor_prefix": "DRIVING",
      "statement_descriptor_prefix_kanji": null,
      "statement_descriptor_prefix_kana": null
    },
    "crypto_payments": {
      "tos_acceptances": {
        "date": null,
        "ip": null
      }
    },
    "dashboard": {
      "display_name": "accessible.stripe",
      "timezone": "Etc/UTC"
    },
    "invoices": {
      "default_account_tax_ids": null,
      "hosted_payment_method_save": "offer"
    },
    "konbini_payments": {},
    "mass_payouts": {
      "tos_acceptance": {
        "date": null,
        "ip": null
      }
    },
    "payments": {
      "statement_descriptor": "ACCESSIBLE.STRIPE.COM",
      "statement_descriptor_kana": null,
      "statement_descriptor_kanji": null
    },
    "payouts": {
      "debit_negative_balances": false,
      "schedule": {
        "delay_days": 2,
        "interval": "daily"
      },
      "statement_descriptor": null
    },
    "sepa_debit_payments": {},
    "tax_forms": {
      "consented_to_paperless_delivery": false
    },
    "treasury": {
      "additional_partners": [],
      "tos_acceptance": {
        "date": null,
        "ip": null
      }
    }
  },
  "stripe_owns_card_payments_pricing": false,
  "stripe_owns_instant_payouts_pricing": false,
  "stripe_owns_lpm_payments_pricing": false,
  "stripe_owns_onboarding": false,
  "test_connected_account_can_bypass_charges_enabled": false,
  "tos_acceptance": {
    "date": 1752512515,
    "ip": "140.54.99.164",
    "user_agent": null
  },
  "type": "custom"
}
```


### 3b. Create a “destination” charge for a Lyft ride in which the rider pays $20 and the driver receives $15. Provide the Payment Intent ID.

Docs referenced:
- https://docs.stripe.com/connect/destination-charges?platform=web&ui=stripe-hosted
- https://docs.stripe.com/api/checkout/sessions

**Payment Intent Id:** pi_3RlB48B3KTBdesMM1ctACLhR<br>
**Checkout Session Id:** cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST

```
stripe checkout sessions create --payment-intent-data.application-fee-amount=500 --payment-intent-data.capture-method="manual" --payment-intent-data.description="Lyft Ride" --payment-intent-data.transfer-data.destination="acct_1RlAGqPnLlHhkn0m" --mode="payment" --customer="cus_SgVtCz2hmBGNKK" --success-url="https://example.com/return?session_id={CHECKOUT_SESSION_ID}" -d "line_items[0][price_data][currency]=USD" -d "line_items[0][price_data][product_data][description]=Ride to Union Station" -d "line_items[0][price_data][product_data][name]=Lyft Ride" -d "line_items[0][price_data][unit_amount]=2000" -d "line_items[0][quantity]=1"
```

Result

```json
{
  "id": "cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST",
  "object": "checkout.session",
  "adaptive_pricing": {
    "enabled": true
  },
  "after_expiration": null,
  "allow_promotion_codes": null,
  "amount_subtotal": 2000,
  "amount_total": 2000,
  "automatic_tax": {
    "enabled": false,
    "liability": null,
    "provider": null,
    "status": null
  },
  "billing_address_collection": null,
  "cancel_url": null,
  "client_reference_id": null,
  "client_secret": null,
  "collected_information": {
    "shipping_details": null
  },
  "consent": null,
  "consent_collection": null,
  "created": 1752592571,
  "currency": "usd",
  "currency_conversion": null,
  "custom_fields": [],
  "custom_text": {
    "after_submit": null,
    "shipping_address": null,
    "submit": null,
    "terms_of_service_acceptance": null
  },
  "customer": "cus_SgVtCz2hmBGNKK",
  "customer_creation": null,
  "customer_details": {
    "address": null,
    "email": "foster+TAM@gmail.com",
    "name": null,
    "phone": null,
    "tax_exempt": "none",
    "tax_ids": null
  },
  "customer_email": null,
  "discounts": [],
  "expires_at": 1752678970,
  "invoice": null,
  "invoice_creation": {
    "enabled": false,
    "invoice_data": {
      "account_tax_ids": null,
      "custom_fields": null,
      "description": null,
      "footer": null,
      "issuer": null,
      "metadata": {},
      "rendering_options": null
    }
  },
  "livemode": false,
  "locale": null,
  "metadata": {},
  "mode": "payment",
  "origin_context": null,
  "payment_intent": null,
  "payment_link": null,
  "payment_method_collection": "if_required",
  "payment_method_configuration_details": {
    "id": "pmc_1RjkR0B3KTBdesMMGbArMg9i",
    "parent": null
  },
  "payment_method_options": {
    "card": {
      "request_three_d_secure": "automatic"
    }
  },
  "payment_method_types": [
    "card",
    "link",
    "cashapp"
  ],
  "payment_status": "unpaid",
  "permissions": null,
  "phone_number_collection": {
    "enabled": false
  },
  "recovered_from": null,
  "saved_payment_method_options": {
    "allow_redisplay_filters": [
      "always"
    ],
    "payment_method_remove": "disabled",
    "payment_method_save": null
  },
  "setup_intent": null,
  "shipping_address_collection": null,
  "shipping_cost": null,
  "shipping_options": [],
  "status": "open",
  "submit_type": null,
  "subscription": null,
  "success_url": "https://example.com/return?session_id={CHECKOUT_SESSION_ID}",
  "total_details": {
    "amount_discount": 0,
    "amount_shipping": 0,
    "amount_tax": 0
  },
  "ui_mode": "hosted",
  "url": "https://checkout.stripe.com/c/pay/cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST#fidkdWxOYHwnPyd1blpxYHZxWjA0V29uVFNHNk5RR2FgdkhITXBdaHxARzx3TE1sTHVcN211cDFcYG43YHxifVF0bE5nd2QwNDNJSHEzYnBCcUl8d3BsaEhtVX1udT01NWQ0TXJiQU1jT2IwNTUybFFUa39vbScpJ2N3amhWYHdzYHcnP3F3cGApJ2lkfGpwcVF8dWAnPyd2bGtiaWBabHFgaCcpJ2BrZGdpYFVpZGZgbWppYWB3dic%2FcXdwYHgl",
  "wallet_options": null
}
```

The Payment Intent Id is not created until the checkout is completed, since the checkout session is still open.

Docs Referenced:
- https://docs.stripe.com/connect/destination-charges?platform=web&ui=stripe-hosted#handle-post-payment-events
- https://docs.stripe.com/checkout/quickstart#testing

Using the test Visa card (**4242), I completed the checkout through my browser at the [Stripe Checkout URL](https://checkout.stripe.com/c/pay/cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST#fidkdWxOYHwnPyd1blpxYHZxWjA0V29uVFNHNk5RR2FgdkhITXBdaHxARzx3TE1sTHVcN211cDFcYG43YHxifVF0bE5nd2QwNDNJSHEzYnBCcUl8d3BsaEhtVX1udT01NWQ0TXJiQU1jT2IwNTUybFFUa39vbScpJ2N3amhWYHdzYHcnP3F3cGApJ2lkfGpwcVF8dWAnPyd2bGtiaWBabHFgaCcpJ2BrZGdpYFVpZGZgbWppYWB3dic%2FcXdwYHgl)

Double checking that the checkout session is complete, and then I can retrieve the Payment Intent Id

```
stripe checkout sessions retrieve cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST
```

Result

```json
{
  "id": "cs_test_a195W8jpnVB4sJt82Ob9sUNxugPAtoLcXyVkqZar5E1LkGgx1SQtbTPmST",
  "object": "checkout.session",
  "adaptive_pricing": {
    "enabled": true
  },
  "after_expiration": null,
  "allow_promotion_codes": null,
  "amount_subtotal": 2000,
  "amount_total": 2000,
  "automatic_tax": {
    "enabled": false,
    "liability": null,
    "provider": null,
    "status": null
  },
  "billing_address_collection": null,
  "cancel_url": null,
  "client_reference_id": null,
  "client_secret": null,
  "collected_information": {
    "shipping_details": null
  },
  "consent": null,
  "consent_collection": null,
  "created": 1752592571,
  "currency": "usd",
  "currency_conversion": null,
  "custom_fields": [],
  "custom_text": {
    "after_submit": null,
    "shipping_address": null,
    "submit": null,
    "terms_of_service_acceptance": null
  },
  "customer": "cus_SgVtCz2hmBGNKK",
  "customer_creation": null,
  "customer_details": {
    "address": {
      "city": null,
      "country": "US",
      "line1": null,
      "line2": null,
      "postal_code": "12345",
      "state": null
    },
    "email": "foster+TAM@gmail.com",
    "name": "Foster Schlienz",
    "phone": null,
    "tax_exempt": "none",
    "tax_ids": []
  },
  "customer_email": null,
  "discounts": [],
  "expires_at": 1752678970,
  "invoice": null,
  "invoice_creation": {
    "enabled": false,
    "invoice_data": {}
  },
  "livemode": false,
  "locale": null,
  "metadata": {},
  "mode": "payment",
  "origin_context": null,
  "payment_intent": "pi_3RlB48B3KTBdesMM1ctACLhR",
  "payment_link": null,
  "payment_method_collection": "if_required",
  "payment_method_configuration_details": {
    "id": "pmc_1RjkR0B3KTBdesMMGbArMg9i",
    "parent": null
  },
  "payment_method_options": {
    "card": {
      "request_three_d_secure": "automatic"
    }
  },
  "payment_method_types": [
    "card",
    "link",
    "cashapp"
  ],
  "payment_status": "unpaid",
  "permissions": null,
  "phone_number_collection": {
    "enabled": false
  },
  "recovered_from": null,
  "saved_payment_method_options": {
    "allow_redisplay_filters": [
      "always"
    ],
    "payment_method_remove": "disabled",
    "payment_method_save": null
  },
  "setup_intent": null,
  "shipping_address_collection": null,
  "shipping_cost": null,
  "shipping_options": [],
  "status": "complete",
  "submit_type": null,
  "subscription": null,
  "success_url": "https://example.com/return?session_id={CHECKOUT_SESSION_ID}",
  "total_details": {
    "amount_discount": 0,
    "amount_shipping": 0,
    "amount_tax": 0
  },
  "ui_mode": "hosted",
  "url": null,
  "wallet_options": null
}
```

### 3c. For this ride, how much is Lyft’s platform fee?

Docs referenced: https://docs.stripe.com/api/application_fees/retrieve

  **Application_fee_amount:** 500 ($5.00)

```
stripe payment_intents retrieve pi_3RlB48B3KTBdesMM1ctACLhR --expand="application_fee_amount
```

Result:

```json
{
  "id": "pi_3RlB48B3KTBdesMM1ctACLhR",
  "object": "payment_intent",
  "amount": 2000,
  "amount_capturable": 0,
  "amount_details": {
    "tip": {}
  },
  "amount_received": 2000,
  "application": null,
  "application_fee_amount": 500,
  "automatic_payment_methods": null,
  "canceled_at": null,
  "cancellation_reason": null,
  "capture_method": "manual",
  "charges": {
    "object": "list",
    "data": [
      {
        "id": "ch_3RlB48B3KTBdesMM1YtOY7qM",
        "object": "charge",
        "amount": 2000,
        "amount_captured": 2000,
        "amount_refunded": 0,
        "application": null,
        "application_fee": "fee_1RlDDXPnLlHhkn0m6Q797bFL",
        "application_fee_amount": 500,
        "balance_transaction": "txn_3RlB48B3KTBdesMM1aQEmTGw",
        "billing_details": {
          "address": {
            "city": null,
            "country": "US",
            "line1": null,
            "line2": null,
            "postal_code": "12345",
            "state": null
          },
          "email": "foster+TAM@gmail.com",
          "name": "Foster Schlienz",
          "phone": null,
          "tax_id": null
        },
        "calculated_statement_descriptor": "Stripe",
        "captured": true,
        "created": 1752594408,
        "currency": "usd",
        "customer": "cus_SgVtCz2hmBGNKK",
        "description": "Lyft Ride",
        "destination": "acct_1RlAGqPnLlHhkn0m",
        "dispute": null,
        "disputed": false,
        "failure_balance_transaction": null,
        "failure_code": null,
        "failure_message": null,
        "fraud_details": {},
        "invoice": null,
        "livemode": false,
        "metadata": {},
        "on_behalf_of": null,
        "order": null,
        "outcome": {},
        "paid": true,
        "payment_intent": "pi_3RlB48B3KTBdesMM1ctACLhR",
        "payment_method": "pm_1RlB47B3KTBdesMMY2wCnc0B",
        "payment_method_details": {
          "card": {},
          "type": "card"
        },
        "radar_options": {},
        "receipt_email": null,
        "receipt_number": null,
        "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xUmprUVZCM0tUQmRlc01NKNG73MMGMgat4tPY9vw6LBaRrzjZpClbAMqoG-TuDAlKyeiPOjUQKhEvd9q6GxVrD7T3Ar8X7btJe-i7",
        "refunded": false,
        "review": null,
        "shipping": null,
        "source": null,
        "source_transfer": null,
        "statement_descriptor": null,
        "statement_descriptor_suffix": null,
        "status": "succeeded",
        "transfer": "tr_3RlB48B3KTBdesMM1WWyZ4Ey",
        "transfer_data": {
          "amount": null,
          "destination": "acct_1RlAGqPnLlHhkn0m"
        },
        "transfer_group": "group_pi_3RlB48B3KTBdesMM1ctACLhR"
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/charges?payment_intent=pi_3RlB48B3KTBdesMM1ctACLhR"
  },
  "client_secret": "pi_3RlB48B3KTBdesMM1ctACLhR_secret_7aTDlwXnvMrSgGukqJah8gqDP",
  "confirmation_method": "automatic",
  "created": 1752594408,
  "currency": "usd",
  "customer": "cus_SgVtCz2hmBGNKK",
  "description": "Lyft Ride",
  "invoice": null,
  "last_payment_error": null,
  "latest_charge": "ch_3RlB48B3KTBdesMM1YtOY7qM",
  "livemode": false,
  "metadata": {},
  "next_action": null,
  "on_behalf_of": null,
  "payment_method": "pm_1RlB47B3KTBdesMMY2wCnc0B",
  "payment_method_configuration_details": null,
  "payment_method_options": {
    "card": {
      "installments": null,
      "mandate_options": null,
      "network": null,
      "request_three_d_secure": "automatic"
    }
  },
  "payment_method_types": [
    "card"
  ],
  "processing": null,
  "receipt_email": null,
  "review": null,
  "setup_future_usage": null,
  "shipping": null,
  "source": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": {
    "destination": "acct_1RlAGqPnLlHhkn0m"
  },
  "transfer_group": "group_pi_3RlB48B3KTBdesMM1ctACLhR"
}

```

 ### 3d. How much is the Stripe processing fee for this ride?

  Docs referenced: [expanding Payment Intents](https://docs.stripe.com/api/expanding_objects#:~:text=You%20can%20expand%20recursively%20by%20specifying%20nested%20fields%20after%20a%20dot%20(.).%20For%20example%2C%20requesting%20payment_intent.customer%20on%20a%20charge%20expands%20the%20payment_intent%20property%20into%20a%20full) and [stackoverflow](https://stackoverflow.com/questions/71605052/obtain-the-stripe-fee-from-payment-intent) for context

**Stripes Processing Fee:** 88 ($0.88)

```
stripe payment_intents retrieve pi_3RlB48B3KTBdesMM1ctACLhR --expand=charges.data.balance_transaction
```

Result:

```json
{
  "id": "pi_3RlB48B3KTBdesMM1ctACLhR",
  "object": "payment_intent",
  "amount": 2000,
  "amount_capturable": 0,
  "amount_details": {
    "tip": {}
  },
  "amount_received": 2000,
  "application": null,
  "application_fee_amount": 500,
  "automatic_payment_methods": null,
  "canceled_at": null,
  "cancellation_reason": null,
  "capture_method": "manual",
  "charges": {
    "object": "list",
    "data": [
      {
        "id": "ch_3RlB48B3KTBdesMM1YtOY7qM",
        "object": "charge",
        "amount": 2000,
        "amount_captured": 2000,
        "amount_refunded": 0,
        "application": null,
        "application_fee": "fee_1RlDDXPnLlHhkn0m6Q797bFL",
        "application_fee_amount": 500,
        "balance_transaction": {
          "id": "txn_3RlB48B3KTBdesMM1aQEmTGw",
          "object": "balance_transaction",
          "amount": 2000,
          "available_on": 1753142400,
          "balance_type": "payments",
          "created": 1752602678,
          "currency": "usd",
          "description": "Lyft Ride",
          "exchange_rate": null,
          "fee": 88,
          "fee_details": [
            {
              "amount": 88,
              "application": null,
              "currency": "usd",
              "description": "Stripe processing fees",
              "type": "stripe_fee"
            }
          ],
          "net": 1912,
          "reporting_category": "charge",
          "source": "ch_3RlB48B3KTBdesMM1YtOY7qM",
          "status": "pending",
          "type": "charge"
        },
        "billing_details": {
          "address": {
            "city": null,
            "country": "US",
            "line1": null,
            "line2": null,
            "postal_code": "12345",
            "state": null
          },
          "email": "foster+TAM@gmail.com",
          "name": "Foster Schlienz",
          "phone": null,
          "tax_id": null
        },
        "calculated_statement_descriptor": "Stripe",
        "captured": true,
        "created": 1752594408,
        "currency": "usd",
        "customer": "cus_SgVtCz2hmBGNKK",
        "description": "Lyft Ride",
        "destination": "acct_1RlAGqPnLlHhkn0m",
        "dispute": null,
        "disputed": false,
        "failure_balance_transaction": null,
        "failure_code": null,
        "failure_message": null,
        "fraud_details": {},
        "invoice": null,
        "livemode": false,
        "metadata": {},
        "on_behalf_of": null,
        "order": null,
        "outcome": {},
        "paid": true,
        "payment_intent": "pi_3RlB48B3KTBdesMM1ctACLhR",
        "payment_method": "pm_1RlB47B3KTBdesMMY2wCnc0B",
        "payment_method_details": {
          "card": {},
          "type": "card"
        },
        "radar_options": {},
        "receipt_email": null,
        "receipt_number": null,
        "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xUmprUVZCM0tUQmRlc01NKPLS2sMGMgZNGCKrdKM6LBbSQS_XhdSIQF0Wa51rBRBHeWSHFIVJ-gA8u4Qa-up2IHRRNXwjQ8sMQN4M",
        "refunded": false,
        "review": null,
        "shipping": null,
        "source": null,
        "source_transfer": null,
        "statement_descriptor": null,
        "statement_descriptor_suffix": null,
        "status": "succeeded",
        "transfer": "tr_3RlB48B3KTBdesMM1WWyZ4Ey",
        "transfer_data": {
          "amount": null,
          "destination": "acct_1RlAGqPnLlHhkn0m"
        },
        "transfer_group": "group_pi_3RlB48B3KTBdesMM1ctACLhR"
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/charges?payment_intent=pi_3RlB48B3KTBdesMM1ctACLhR"
  },
  "client_secret": "pi_3RlB48B3KTBdesMM1ctACLhR_secret_7aTDlwXnvMrSgGukqJah8gqDP",
  "confirmation_method": "automatic",
  "created": 1752594408,
  "currency": "usd",
  "customer": "cus_SgVtCz2hmBGNKK",
  "description": "Lyft Ride",
  "invoice": null,
  "last_payment_error": null,
  "latest_charge": "ch_3RlB48B3KTBdesMM1YtOY7qM",
  "livemode": false,
  "metadata": {},
  "next_action": null,
  "on_behalf_of": null,
  "payment_method": "pm_1RlB47B3KTBdesMMY2wCnc0B",
  "payment_method_configuration_details": null,
  "payment_method_options": {
    "card": {
      "installments": null,
      "mandate_options": null,
      "network": null,
      "request_three_d_secure": "automatic"
    }
  },
  "payment_method_types": [
    "card"
  ],
  "processing": null,
  "receipt_email": null,
  "review": null,
  "setup_future_usage": null,
  "shipping": null,
  "source": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": {
    "destination": "acct_1RlAGqPnLlHhkn0m"
  },
  "transfer_group": "group_pi_3RlB48B3KTBdesMM1ctACLhR"
}
```

### 3e. What are Lyft's net earnings for this ride? ###

Notes:
- The application fee amount is transferred to the platform, and the Stripe fee is deducted from the platform’s amount

Docs referenced: 
- [Destination charges and fees](https://docs.stripe.com/connect/destination-charges?platform=web&ui=stripe-hosted#:~:text=the%20Stripe%20fee%20is%20deducted%20from%20the%20platform%E2%80%99s%20amount)
- [Collect Fees](https://docs.stripe.com/connect/collect-then-transfer-guide#collect-fees)
```
stripe application_fees retrieve fee_1RlDDXPnLlHhkn0m6Q797bFL --expand="balance_transaction"
```

```json
{
  "id": "fee_1RlDDXPnLlHhkn0m6Q797bFL",
  "object": "application_fee",
  "account": "acct_1RlAGqPnLlHhkn0m",
  "amount": 500,
  "amount_refunded": 0,
  "application": "ca_SfWCukTAwoQrNQGdUiFtL3PpdJrRBndd",
  "balance_transaction": {
    "id": "txn_1RlDDZB3KTBdesMMUDWiUtDA",
    "object": "balance_transaction",
    "amount": 500,
    "available_on": 1753142400,
    "balance_type": "payments",
    "created": 1752602679,
    "currency": "usd",
    "description": "Application fee from application Foster Test sandbox for connect+test@gmail.com (acct_1RlAGqPnLlHhkn0m)",
    "exchange_rate": null,
    "fee": 0,
    "fee_details": [],
    "net": 500,
    "reporting_category": "platform_earning",
    "source": "fee_1RlDDXPnLlHhkn0m6Q797bFL",
    "status": "pending",
    "type": "application_fee"
  },
  "charge": "py_1RlDDXPnLlHhkn0m8Y90QRE3",
  "created": 1752602679,
  "currency": "usd",
  "fee_source": {
    "charge": "py_1RlDDXPnLlHhkn0m8Y90QRE3",
    "type": "charge"
  },
  "livemode": false,
  "originating_transaction": "ch_3RlB48B3KTBdesMM1YtOY7qM",
  "refunded": false,
  "refunds": {
    "object": "list",
    "data": [],
    "has_more": false,
    "total_count": 0,
    "url": "/v1/application_fees/fee_1RlDDXPnLlHhkn0m6Q797bFL/refunds"
  }
}
```


### 3f. Now, try to have Lyft charge the driver $2 to cover the cost of the neon-lighted Lyft sign that sits in their dashboard. Provide the ID for that request. ###

Docs referenced: [Charge a connect account](https://docs.stripe.com/connect/account-debits?dashboard-or-api=api#transferring-from-a-connected-account:~:text=Charge%20a%20connected%20account)

**Payment Id:** py_1RlEayB3KTBdesMMUuSPHFj0

```
stripe charges create --description="Direct charge for Lyft neon sign" --currency="USD" --amount=200 --source="acct_1RlAGqPnLlHhkn0m"
```

Result:

```json
{
  "id": "py_1RlEayB3KTBdesMMUuSPHFj0",
  "object": "charge",
  "amount": 200,
  "amount_captured": 200,
  "amount_refunded": 0,
  "application": "ca_SfWCukTAwoQrNQGdUiFtL3PpdJrRBndd",
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_1RlEazB3KTBdesMMMLJPQJg6",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null,
    "tax_id": null
  },
  "calculated_statement_descriptor": null,
  "captured": true,
  "created": 1752607976,
  "currency": "usd",
  "customer": null,
  "description": "Direct charge for Lyft neon sign",
  "destination": null,
  "dispute": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "order": null,
  "outcome": {
    "advice_code": null,
    "network_advice_code": null,
    "network_decline_code": null,
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "not_assessed",
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": null,
  "payment_method_details": {
    "stripe_account": {},
    "type": "stripe_account"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xUmprUVZCM0tUQmRlc01NKOnZ2sMGMgZFJy6fnO86LBbGqIklaDExXxTpMkrpxm8wMf3EGGFnYbdWFl7Ty1OzS8hGCiy7MkVBciwp",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source": {
    "id": "acct_1RlAGqPnLlHhkn0m",
    "object": "account"
  },
  "source_transfer": "tr_1RlEayPnLlHhkn0mWAhazoRx",
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

### 3g. Tell us about how you went about solving 3F. What is your API call doing? ###

To solve 3F, Lyft needs charge the driver (connect account) $2.00 for a neon-light sign. This required creating a direct charge to the driver’s Connect Account.

**Steps Taken**

I used the Charge endpoint to create a charge directly on the driver’s connected account. The command was:

```
stripe charges create --description="Direct charge for Lyft neon sign" --currency="USD" --amount=200 --source="acct_1RlAGqPnLlHhkn0m"
```

Parameters:
- description: Provided a reason for the charge (“Direct charge for Lyft neon sign”)
- currency: Set to USD, the same as the Connect Account
- amount: Set to 200 (which represents $2.00)
- source: The connected account ID for the driver

The docs I used to learn how to complete this question: https://docs.stripe.com/connect/account-debits?dashboard-or-api=api#charging-a-connected-account

---

### 3h. Aside from rideshare, name a business or industry that should use Stripe Connect and why ###

Vrbo is a good example of a company that should use Stripe Connect because it has the exact challenges that Connect was designed to solve.

**Why**

Vrbo is a two-sided marketplace (ie. a buyer and a seller) providing services to both guests and hosts worldwide. Some key challenges that Vrbo would face are:
- Payments/fees: Vrbo needs to collect payments from Hosts, and then distribute to hosts. Each Host might choose to accept a different payout method
- Jurisdiction support: Vrbo is in over 200 countries, and needs a payments processor that can support multiple currencies and payouts schedules/methods
- With the size of Vrbo's user base, having an easy to follow onboarding flow for new users is critical to maintain positive user experiences


**How Stripe is a good fit**

When a guest makes a booking, Stripe Connect can:
- Instantly collect the full amount from the guest (https://docs.stripe.com/connect/instant-payouts)
- Automatically deduct platform fees, service charges, and applicable taxes (https://docs.stripe.com/connect/invoices#collecting-fees)

When a new Host wants to join Vrbo, Stripe Connect can:
- Offer a flexible onboarding experience for new Hosts: https://docs.stripe.com/connect/onboarding
- Handle KYC and updates on behalf of Vrbo (https://docs.stripe.com/connect/identity-verification)

When a customer wants to pay in a different currency than the platforms', Stripe can:
- Offer a multi-currency payout system, opening up new markets for a host (https://docs.stripe.com/payouts/multicurrency-settlement?account-country=US#multicurrency-settlement-fees)
- Allow Hosts to choose their preferred payout schedule (https://docs.stripe.com/payouts#:~:text=Subsequent%20payouts%20follow%20your%20account%E2%80%99s%20payout%20schedule)
  
**Summary**
Stripe Connect is a great fit for Vrbo and other short-term rental marketplaces due to it's capabilities to provide different payout methods, easy KYC and onboarding flows, and multi-currency payouts schemes. Almost any global marketplace, whether it's for short-term rentals or even something like Ebay, would gain huge efficiency and trust from it's users! 
  

## Question 4 | Responding to Users


_"Good news, we got go ahead for our planned streaming service. Development will start next week and we’re looking to understand how we can charge our users on a monthly basis, it looks like Stripe can help with that?_

_We have two plans in mind:_
- _Plan A: Flat rate of $24.99 per month for unlimited usage of the service_
- _Plan B: $10.99 for the first 100 GB and $1.00 per subsequent 10 GB_
  
_Can you please give an overview of how this could be achieved through the API? As you know, we use Python in our environment, so if you could share the API calls with the required parameters needed, that'd be great._

_Finally, if we wanted to introduce a coupon into the mix, how would that work?_


### 4. How would you respond?

Hey [Customer], thanks for reaching out. Happy to help walk you through how to get subscriptions set up for your streaming platform.

Before you get started, make sure you have the Stripe client in your [environment](https://docs.stripe.com/billing/subscriptions/build-subscriptions?platform=web&ui=stripe-hosted&lang=python#set-up-stripe).

Here's a step by step process for creating Plan A (you can use these [Docs](https://docs.stripe.com/products-prices/pricing-models?dashboard-or-api=api#flat-rate) as a reference guide):

1. First, create the product:

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"
product = stripe.Product.create(name="Plan A")
```

2. Once the product is created, you can add the price by [referencing the Product id](https://docs.stripe.com/products-prices/pricing-models?dashboard-or-api=api&lang=python#flat-rate:~:text=Create%20the%20monthly%20price%20for%20the%20Basic%20product):

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"

price = stripe.Price.create(
  product="{{PRODUCT_ID}}",
  currency="usd",
  unit_amount=2499,  # $24.99 in cents
  billing_scheme="per_unit",
  recurring={"usage_type": "licensed", "interval": "month"},
)

```

Here's a step by step process for creating Plan B (you can use these [Docs](https://docs.stripe.com/products-prices/pricing-models?dashboard-or-api=api#usage-based-pricing) as a reference guide):

1. First, create the product:

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"
product = stripe.Product.create(name="Plan B")
```

2. Create the price for the first 100GB:

```py
price_base = stripe.Price.create(
  product="{{PRODUCT_ID}}",
  currency="usd",
  unit_amount=1099,  # $10.99
  billing_scheme="per_unit",
  recurring={"usage_type": "licensed", "interval": "month"},
)
```

3. Next, create the Tiered price (here are the [docs](https://docs.stripe.com/products-prices/pricing-models?dashboard-or-api=api#usage-based-pricing:~:text=For%20the%20second%20tier%2C%20specify%200.001%20USD%20per%20unit.%20The%20first%20tier%20has%20a%20price%20of%200%20USD%20because%20the%20flat%20rate%20includes%20the%20first%20100%2C000%20units.) for reference)

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"

price = stripe.Price.create(
  product="{{PRODUCT_ID}}",
  currency="usd",
  billing_scheme="tiered",
  recurring={
    "usage_type": "metered",
    "interval": "month"
  },
  tiers_mode="volume",
  tiers=[
    {"up_to": 1000, "unit_amount_decimal": "0"},  # price is set to 0 since the flat rate already covers that first 100GB
    {"up_to": "inf", "unit_amount_decimal": "10"}    # $1.00 per 10 GB → $0.10 per 1 GB → 10 cents per unit
  ],
  transform_quantity={"divide_by": 10, "round": "up"}  # Each unit = 10 GB
)
```

Since Stripe cannot recognize GB as a unit, you can use the [transform quantity option](https://docs.stripe.com/billing/subscriptions/usage-based/transform-quantities) to a price before billing your customers.

You can now pass either of these Product Id's when you create a new subscription on your streaming platform:

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"

subscription = stripe.Subscription.create(
  customer="{{CUSTOMER_ID}}",
  items=[
    {"price": "{{FLAT_MONTHLY_FEE_PRICE_ID}}", "quantity": 1},
    {"price": "{{METERED_USAGE_PRICE_ID}}"},
  ],
)
```

Lastly, adding a coupon is straight forward! Here's the [documentation on how to create a coupon](https://docs.stripe.com/billing/subscriptions/coupons#coupons), and an example API call of what this would look like:

```py
import stripe
stripe.api_key = "sk_test_51LYFTEK59E4LUfA95u9dDKQZAZi9Mo2naEtvobUW2h3tVjAOZrnj5pbMXHQkfhZYMK2PQKAKE7Tp3uLAntjrCivY00XbHzq4cq"

subscription = stripe.Subscription.create(
  customer="{{CUSTOMER_ID}}",
  items=[
    {"price": "{{FLAT_MONTHLY_FEE_PRICE_ID}}", "quantity": 1},
    {"price": "{{METERED_USAGE_PRICE_ID}}"},
  ],
   coupon="COUPON_ID"
)
```

I hope this was helpful! If you require any further assistance, let me know and I'd be happy to schedule a session to walk through this together.

With regards,

Foster

---