# Fix: EAS Permissions Error

## The Problem

Error: `Entity not authorized: AppEntity[975f4b67-4792-44df-8968-d4458641ed01]`

You're logged in as `annedithb` but the EAS project belongs to `dreamswonder` account.

## Solution: Switch to dreamswonder Account

You have access to `dreamswonder` account (Role: Developer), so switch to it:

### Step 1: Logout and Login as dreamswonder

```bash
eas logout
eas login
```

When prompted:
- **Email/Username**: Use the email for `dreamswonder` account
- **Password**: Enter password for that account

### Step 2: Verify You're on the Right Account

```bash
eas whoami
```

Should show: `dreamswonder` (not `annedithb`)

### Step 3: Try Build Again

```bash
eas build --platform ios --profile preview
```

## Alternative: Use dreamswonder Account Directly

If you know the credentials for `dreamswonder`:

```bash
eas login --username dreamswonder
```

Or login with the email associated with `dreamswonder` account.

## Why This Happened

The EAS project ID `975f4b67-4792-44df-8968-d4458641ed01` was created under the `dreamswonder` account. You need to be logged in as that account (or have Owner/Admin permissions) to build.

## After Switching Accounts

Once logged in as `dreamswonder`:
- ✅ You'll have access to the EAS project
- ✅ Builds will work
- ✅ You can manage the project

## Summary

**The fix**: Log in as `dreamswonder` account instead of `annedithb`.

```bash
eas logout
eas login
# Enter dreamswonder credentials
eas build --platform ios --profile preview
```

🚀

