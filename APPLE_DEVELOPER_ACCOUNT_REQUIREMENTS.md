# Apple Developer Account Requirements for iOS Builds

## Important: You Need an Apple Developer Account

**For ANY iOS build (including TestFlight), you MUST have:**
- An **Apple Developer Program membership** ($99/year)
- This is required by Apple, not Expo/EAS

## Your Options

### Option 1: Use Organization's Apple Developer Account (Best)

If `dreamswonder` has an Apple Developer account, you can use it:

#### Step 1: Get Access to the EAS Project

Ask `dreamswonder` to:
1. Go to https://expo.dev/accounts/dreamswonder/projects
2. Open the project (ID: `975f4b67-4792-44df-8968-d4458641ed01`)
3. Settings → Members → Add `annedithb` with proper permissions
4. Or share the Apple Developer credentials with you

#### Step 2: Build Using Their Account

When you run the build, EAS will prompt for Apple Developer credentials:
- Use `dreamswonder`'s Apple ID
- Use their password
- Enter 2FA code when prompted

**This way:**
- ✅ You can build under your Expo account
- ✅ Use their Apple Developer account
- ✅ No need for your own $99 subscription

### Option 2: Create New EAS Project + Use Their Apple Account

Even with a new EAS project, you can still use `dreamswonder`'s Apple Developer account:

1. **Create new EAS project** (under your `annedithb` account)
2. **When building**, EAS will ask for Apple Developer credentials
3. **Enter `dreamswonder`'s Apple Developer credentials**

This works because:
- EAS project = Expo account (your `annedithb` account)
- Apple Developer = Separate (can be `dreamswonder`'s)

### Option 3: Get Your Own Apple Developer Account

If you need your own:
1. Go to https://developer.apple.com/programs/
2. Sign up for Apple Developer Program ($99/year)
3. Wait for approval (usually instant, sometimes 24-48 hours)
4. Then you can build independently

## Recommended Solution

**Use Option 1 or 2** - both allow you to use `dreamswonder`'s Apple Developer account:

### If You Can Access the EAS Project:

```bash
# Stay logged in as annedithb
# Ask dreamswonder to add you to the project
# Then build:
eas build --platform ios --profile preview
# When prompted, enter dreamswonder's Apple Developer credentials
```

### If You Create New EAS Project:

```bash
# 1. Remove hardcoded project ID from app.config.js
# 2. Configure new project
eas build:configure

# 3. Build (will prompt for Apple credentials)
eas build --platform ios --profile preview
# Enter dreamswonder's Apple Developer credentials when prompted
```

## What EAS Needs from Apple Developer Account

When building, EAS will ask for:
1. **Apple ID** (email associated with Apple Developer account)
2. **Password**
3. **2FA Code** (if enabled)
4. **Team ID** (auto-detected)

You can use `dreamswonder`'s credentials for all of these.

## Summary

**You don't need your own Apple Developer account if:**
- ✅ You can use `dreamswonder`'s Apple Developer account
- ✅ They share the credentials with you
- ✅ Or they add you to their Apple Developer team

**You DO need Apple Developer account if:**
- ❌ You want to build independently
- ❌ No one will share credentials with you
- ❌ You need your own App Store listing

## Next Steps

1. **Ask `dreamswonder`** for their Apple Developer account credentials
2. **OR** ask them to add you to the EAS project with proper permissions
3. **Then** proceed with the build

The build will work as long as you have Apple Developer credentials (yours or theirs)! 🚀

