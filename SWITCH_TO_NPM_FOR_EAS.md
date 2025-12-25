# Switch to npm for EAS Builds

## The Problem

EAS build environment doesn't automatically enable Corepack for Yarn 4.x, causing the build to fail with Yarn version mismatch errors.

## The Solution

I've switched the EAS build to use **npm** instead of Yarn. This is simpler and more reliable for EAS builds.

## What I Changed

### 1. Updated `eas.json`
- Removed `"yarn": "4.12.0"`
- Added `"npm": { "enabled": true }`

### 2. Removed `packageManager` from `package.json`
- Removed `"packageManager": "yarn@4.12.0"`
- This allows EAS to use npm without conflicts

## Next Steps

### Step 1: Generate package-lock.json

On your Mac, run:

```bash
cd Belle-transfer-master-fe

# Remove yarn files
rm yarn.lock
rm -rf .yarn

# Install with npm to generate package-lock.json
npm install

# This creates package-lock.json which EAS will use
```

### Step 2: Update .gitignore (if needed)

Make sure `package-lock.json` is NOT in `.gitignore`:

```bash
# Check .gitignore
cat .gitignore | grep package-lock

# If it's listed, remove that line
```

### Step 3: Commit Changes

```bash
git add package.json eas.json package-lock.json
git rm yarn.lock  # Remove yarn.lock
git commit -m "Switch to npm for EAS builds"
git push
```

### Step 4: Rebuild

```bash
eas build --platform ios --profile preview
```

## Why This Works

- **npm is the default** for EAS builds
- **No Corepack needed** - npm works out of the box
- **More reliable** - fewer version conflicts
- **package-lock.json** is automatically used by EAS

## Local Development

You can still use Yarn locally if you want:

```bash
# Locally, you can use yarn
yarn install
yarn start

# But EAS will use npm for builds
```

Or switch everything to npm:

```bash
# Remove yarn
rm yarn.lock
rm -rf .yarn
rm .yarnrc.yml

# Use npm everywhere
npm install
npm start
```

## Alternative: Keep Yarn (More Complex)

If you really want to keep Yarn 4.x for EAS builds, you'd need to:

1. Add a build hook to enable Corepack
2. Configure it in `eas.json`
3. This is more complex and less reliable

**Using npm is the recommended approach** for EAS builds! ✅

## Summary

**The fix**: Switched EAS to use npm instead of Yarn.

**Next steps**:
1. Run `npm install` locally to generate `package-lock.json`
2. Commit and push changes
3. Rebuild with EAS

This should resolve the Yarn version issues! 🚀

