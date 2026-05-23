

## custom domain mapping

To map a custom domain to an application deployed via Google Cloud tools (like Cloud Run or App Engine), you must verify domain ownership, create the resource mapping, and update your domain registrar's DNS records.

### steps to implement

**1. verify domain ownership**

- Before Google Cloud can attach your domain, you must prove that you own it.
- Execute the following command in your terminal to initiate verification:
- `gcloud domains verify example.com`

2. create the domain mapping

3. update the domain registrar DNS records
