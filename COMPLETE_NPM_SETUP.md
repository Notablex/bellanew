# Complete NPM Setup for EAS Builds

## Current Status

✅ **Good News:**
- `package-lock.json` exists
- `yarn.lock` is removed (not in repo)
- `eas.json` configured to use npm
- `.gitignore` doesn't exclude `package-lock.json`

## Final Setup Steps

### Step 1: Verify package-lock.json is Committed

On your Mac, check:

```bash
cd Belle-transfer-master-fe

# Check if package-lock.json is tracked by git
git ls-files | grep package-lock.json

# If nothing shows, add it:
git add package-lock.json
git commit -m "Add package-lock.json for EAS npm builds"
git push
```

### Step 2: Ensure package-lock.json is Up to Date

```bash
# Remove node_modules
rm -rf node_modules

# Clear npm cache
npm cache clean --force

# Reinstall to regenerate package-lock.json
npm install

# Verify package-lock.json was updated
git status
```

If `package-lock.json` changed, commit it:

```bash
git add package-lock.json
git commit -m "Update package-lock.json"
git push
```

### Step 3: Verify eas.json Configuration

Your `eas.json` now has:
```json
"preview": {
  "cli": "npm",  // ✅ Explicitly uses npm
  "node": "20.11.0",
  ...
}
```

This ensures EAS uses npm instead of yarn.

### Step 4: Build with Cache Clear (First Time)

```bash
# Clear EAS build cache
eas build --platform ios --profile preview --clear-cache
```

The `--clear-cache` flag ensures a fresh build without cached dependencies.

## Why This Works

1. **`"cli": "npm"`** in `eas.json` - Explicitly tells EAS to use npm
2. **`package-lock.json`** - EAS uses this for dependency resolution
3. **No `yarn.lock`** - Prevents conflicts
4. **Cache cleared** - Ensures fresh dependency install

## Alternative: Environment Variable

You can also specify npm via environment variable:

```bash
EAS_BUILD_CLI=npm eas build --platform ios --profile preview
```

But having it in `eas.json` is better (persistent configuration).

## Verification Checklist

Before building, verify:

- [ ] `package-lock.json` exists in project root
- [ ] `package-lock.json` is committed to git
- [ ] `yarn.lock` is NOT in the repo
- [ ] `eas.json` has `"cli": "npm"` in preview profile
- [ ] `node_modules` is in `.gitignore` (should be)
- [ ] `package-lock.json` is NOT in `.gitignore` (should NOT be)

## Build Command

Once everything is set up:

```bash
# Standard build
eas build --platform ios --profile preview

# Or with cache clear (if having issues)
eas build --platform ios --profile preview --clear-cache
```

## Troubleshooting

### If Build Still Fails with Dependency Errors

1. **Update package-lock.json locally**:
   ```bash
   rm -rf node_modules
   npm cache clean --force
   npm install
   git add package-lock.json
   git commit -m "Update package-lock.json"
   git push
   ```

2. **Clear EAS cache**:
   ```bash
   eas build --platform ios --profile preview --clear-cache
   ```

3. **Check build logs** in EAS dashboard for specific errors

## Summary

**Your setup is correct!** Just make sure:
1. ✅ `package-lock.json` is committed
2. ✅ `eas.json` has `"cli": "npm"` (already added)
3. ✅ Build with `eas build --platform ios --profile preview`

You're ready to build! 🚀

