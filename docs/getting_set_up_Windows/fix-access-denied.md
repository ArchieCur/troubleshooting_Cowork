# Fix: VM Service Logon / Access Denied

The Cowork Readiness Checker flagged a warning about a **"VM service logon right"** or an **"Access Denied"** error.

This means Windows blocked the checker from reading a security setting that Cowork needs. This is almost always seen on computers managed by an employer.

---

## Is this your personal computer or a work computer?

### 🏠 Personal computer

This warning is uncommon on personal PCs. If you're seeing it on a computer you own and manage yourself, it may be caused by a restrictive local security policy or third-party security software.

**Try this first:**

**1. Run the Cowork Readiness Checker as Administrator**

Sometimes the checker simply needs elevated permissions to read the setting.

- Find the Cowork Readiness Checker application
- Right-click on it
- Select **Run as administrator**
- Run the check again

✅ **Warning gone? You're done — ready to install Cowork!**

❌ **Still seeing the warning?**

The restriction may be set at a deeper level. If you're comfortable with Windows security settings, check your **Local Security Policy**:

- Open the Start menu → type `Local Security Policy` → open it
- Go to **Local Policies → User Rights Assignment**
- Look for **Log on as a service**
- Confirm that the relevant VM service accounts are listed

If you're not comfortable making changes here, consider reaching out to a trusted technical contact for help.

### 🏢 Work computer (managed by an employer)

This is the most common scenario for this warning. Your IT department controls which services are allowed to log on, and Cowork's virtualization services have been blocked by that policy.

This is not something you can fix yourself — your IT department needs to grant the appropriate logon rights.

A pre-written email template is ready for you — it includes the technical details your IT department will need.

👉 [IT email template: VM service logon rights](windows-it-email-templates.md#vm-service-logon-rights)

!!! note "What to expect"
    This is a straightforward change for an IT administrator. If your company has a helpdesk ticketing system, consider submitting a ticket as well as sending the email so your request is tracked.

---

## Still stuck?

👉 [Back to Windows Checker Errors hub](windows-checker-errors.md)  

*ArchieCur created in collaboration with Claude Sonnet 4.6 (Anthropic) · v1.0.0 · June 2026*
