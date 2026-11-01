# Free email subscriptions — review proposal
Prepared 1 November 2026. Status: proposal only; no live form, account creation, subscriber import, confirmation email, campaign, or distribution has been activated.

## Existing site reviewed
Repository: mliontos/Liontos-Weekly-Updates-in-Oncology, main branch.
Reviewed index.html, _config.yml, _layouts/default.html and assets/css/style.css. The live URL could not be retrieved by the research tool; this review is of the current repository source, not a visual browser check of deployment.

Keep the exact title **Weekly Updates in Oncology**, existing SVG banner, edition links, editorial content, and current navy/blue/gold palette. The homepage currently has no subscription mechanism. The Jekyll layout loads a shared stylesheet. GitHub Pages remains the publication home; subscriber records stay with the email provider.

## Recommendation and alternatives
All subscriptions are free for readers. Provider free-plan limits are separate from the reader price.

| Service | Verified free allowance | Suitability |
| --- | --- | --- |
| EmailOctopus Starter | 2,500 subscribers; 10,000 emails/month; 1 form; 1 landing page; 1 user | Recommended for a weekly digest; provider branding remains in emails. |
| MailerLite Free | 250 active subscribers; 2,500 emails/month | Suitable for a small initial list; lower subscriber ceiling. |
| Brevo Free | 300 sends/day | Less convenient for delivering the same weekly issue to a larger list on one day. |

At 2,000 subscribers, five weekly editions use all 10,000 EmailOctopus sends before any other counted messages. At 2,500, four editions exhaust it. Use about 1,800 subscribers as an initial planning threshold, not a provider-imposed limit; monitor the actual quota. Confirm how confirmation/test sends are counted in the account before launch. Recheck plan limits before committing.

Use regular EmailOctopus, not EmailOctopus Connect/Amazon SES. No AWS account is proposed.

## Proposed implementation
1. Add one inline card on the homepage immediately after the banner, before “Latest edition”, using existing `glance`, `eyebrow` and `sourcebtn` styles.
2. Heading: **Get the weekly update — free**.
3. Copy: “Receive Weekly Updates in Oncology by email. Free subscription. Confirm your email to join; unsubscribe at any time.”
4. Collect email only. Add an explicit, unchecked required consent box: “I would like to receive Weekly Updates in Oncology by email.” Include a clearly labelled privacy link.
5. Generate one inline form in EmailOctopus. Match Arial and the existing colours (#082f61, #2d86ad, #eaf6fc); insert only its provider-generated embed at that card. Reuse the same form if later added to edition pages. Do not invent POST URLs or expose an API key in public code.
6. Display “Check your inbox to confirm your subscription” after submission. Do not say “subscribed” before confirmation. The confirmation success screen says “Your free subscription is confirmed.”
7. Enable **double opt-in explicitly** in list → Consent & customisation → Double opt-in email: it is not the default. New form submissions remain Pending until confirmed. Do not import addresses or manually promote Pending contacts.
8. Keep newsletter campaigns, welcome sequences, RSS-to-email and scheduled delivery off. Publishing an article must not send mail. Confirmation messages will begin only after explicit approval to activate the registration flow.
9. Future campaign templates must contain the provider's personalised unsubscribe hyperlink, sender information, and required free-plan branding. Preserve unsubscribed status so future imports cannot silently re-enrol readers.

Proposed confirmation subject: “Confirm your free subscription to Weekly Updates in Oncology”.
Proposed confirmation body: “Please confirm that you would like to receive Weekly Updates in Oncology. If you did not request this subscription, ignore this email.”
Use the provider editor's confirmation button/link; do not hard-code a confirmation token.

## Account setup required from the owner
- Create/approve an EmailOctopus Starter account, verify the account email, and complete any provider account review. No payment card is required for the published free offer.
- Approve the From name (“Michalis Liontos | Weekly Updates in Oncology”), Reply-To address and a valid professional postal address. Do not infer that an institutional mailbox/domain is authorised for this newsletter.
- Select a sender mailbox/domain that the owner is authorised to use. For a domain owned/controlled by the owner, apply the provider's exact DNS authentication records and verify them. The github.io site hostname is not a sender domain the owner controls. Institutional DNS may require IT assistance.
- Create a single audience named “Weekly Updates in Oncology”; enable double opt-in and supply the generated inline form code.
- Approve a concise privacy notice naming the responsible publisher, contact address, provider, data collected, purpose, withdrawal/deletion route and retention policy. Keep personal data out of this public repository.
- Keep account credentials and any private API keys out of GitHub and chat. Use the account interface for sign-in.
- Approve form publication separately from the first newsletter distribution. No campaigns may be sent or scheduled without explicit instruction.

## Launch checks (not yet performed)
After account configuration and explicit authorisation for test confirmation messages, use owner-controlled test addresses only:
- Valid email submits as Pending; required consent cannot be bypassed through the normal form UI.
- Confirmation arrives and changes status to Subscribed only after the link is clicked.
- Invalid addresses, duplicate submissions and unconfirmed addresses behave clearly; no false success message.
- Test the actual personalised unsubscribe flow with an authorised test campaign; verify suppression prevents a second send.
- Verify mobile layout, keyboard navigation, input labels, contrast, status messages and provider-hosted error states.
- Verify the homepage banner/title and all existing edition links remain intact.
- Confirm no auto-send workflow, RSS integration, existing list import or scheduled campaign is enabled.
- Inspect the final diff, then publish the form only when approved. Authorise any first distribution as a distinct action.

No end-to-end email or visual deployment testing has been completed: account configuration and a real provider form are still required.

## Primary sources checked on 1 November 2026
- EmailOctopus pricing: https://emailoctopus.com/pricing
- Form creation and styling: https://help.emailoctopus.com/article/33-forms
- Double opt-in: https://help.emailoctopus.com/article/36-how-to-edit-double-opt-in
- Required footer: https://help.emailoctopus.com/article/222-whats-required-in-a-footer
- Unsubscribe hyperlink: https://help.emailoctopus.com/article/71-how-to-insert-an-unsubscribe-link
- Sender authentication: https://help.emailoctopus.com/article/160-verifying-a-new-domain
- MailerLite free-plan update: https://www.mailerlite.com/help/free-plan-update-faq
- Brevo free limits: https://help.brevo.com/hc/en-us/articles/208580669-FAQs-What-are-the-limits-of-the-Free-plan

The site's title/design review uses repository source. Service limits above use official provider documentation. Account-specific availability and deliverability remain to be checked during setup.
