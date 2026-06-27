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

Cowork requires these **exact service accounts** to start correctly:  

- NT SERVICE\vmcompute  
- NT SERVICE\hns

Those two are the ones Windows uses to run the virtual machine and its networking layer.
If you see only ALL SERVICES, it means the policy was set too broadly.
You’ll need to add the two specific accounts manually.  

**If both are listed:** this fix doesn’t apply— go back and follow the “Hypervisor not running” path. 
**If one or both are missing:** continue to Step 2.

**2. Adding the missing `NT SERVICE\vmcompute` and or `NT SERVICE\hns`**  
- In the Log on as a service window, **click** Add User or Group…
- **Click** Advanced….
- **Click** Find Now.
- In the search results list, scroll until you find:
    **vmcompute**
    **hns**
- **Double click** vmcompute to add it.
- **Repeat for hns.**
- **Click OK** to close each dialog, then **Apply** to save the policy.

**3. – Restart** 
- **Restart your computer** (this matters—policy changes don’t always apply immediately).

**If you see a “Select Users or Groups (Advanced)” dialog during setup, it means Windows cannot access the virtualization components.  
This happens when Virtual Machine Platform is not installed or when the device is restricted by employer security policies. 
Personal computers should not show this dialog.**  

❌ **Seeing “Select Users or Groups (Advanced)”?**  

You will need to Go to **Fix: Virtual Machine Platform is Turned Off** 

If you're not comfortable making changes here, consider reaching out to a trusted technical contact for help.  
---

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
