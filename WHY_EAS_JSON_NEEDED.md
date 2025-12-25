# Why the Preview Profile in eas.json is Needed

## Yes, You Need It! ✅

The preview profile in `eas.json` (lines 11-16) is **essential** for TestFlight builds. Here's why:

### What It Does

```json
"preview": {
  "distribution": "store",        // ✅ App Store distribution (for TestFlight)
  "env": {
    "APP_VARIANT": "preview"       // ✅ Sets environment variable during build
  },
  "ios": {
    "simulator": false,            // ✅ Builds for real devices
    "buildConfiguration": "Release" // ✅ Release build (not debug)
  }
}
```

### Why Each Setting Matters

1. **`"distribution": "store"`**
   - Required for TestFlight/App Store
   - Without it, EAS might try ad-hoc distribution (requires device registration)
   - This is what prevents the device registration error!

2. **`"env": { "APP_VARIANT": "preview" }`**
   - **CRITICAL**: EAS builds don't automatically read `.env` files
   - This ensures `APP_VARIANT=preview` is set during the build
   - This makes the app use `com.dreamswonder.appcita` (not `.dev`)
   - Without this, it defaults to development bundle ID

3. **`"simulator": false`**
   - Builds for real iOS devices (TestFlight)
   - Simulator builds can't be submitted to TestFlight

4. **`"buildConfiguration": "Release"`**
   - Release builds are optimized and required for App Store
   - Debug builds are larger and not suitable for distribution

## The Problem You Were Having

The build was using `com.dreamswonder.appcita.dev` because:
- EAS builds don't read `.env` files automatically
- `APP_VARIANT` wasn't set during the build
- App defaulted to development mode
- Development bundle ID requires device registration

## The Fix

I've added `"env": { "APP_VARIANT": "preview" }` to the preview profile. Now:
- ✅ `APP_VARIANT` is set during the build
- ✅ App uses `com.dreamswonder.appcita` (not `.dev`)
- ✅ No device registration needed
- ✅ Ready for TestFlight

## Summary

**Keep the preview profile!** It's essential. I've just added the `env` section to ensure `APP_VARIANT` is set correctly during builds.

Now when you run:
```bash
eas build --platform ios --profile preview
```

It will:
1. Use the preview profile settings
2. Set `APP_VARIANT=preview` during build
3. Use bundle ID `com.dreamswonder.appcita`
4. Build for App Store distribution
5. **No device registration needed!** ✅

