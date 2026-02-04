# Quick Reference Guide - Proveedores Versiones

## 🚀 Common Commands

### View Current Version
```bash
cat VERSION
```

### View Change History
```bash
cat CHANGELOG.md
```

### List All Versions
```bash
ls -1 versions/ | grep -E '^[0-9]+\.'
```

### View Version Details
```bash
# JSON metadata
cat versions/1.0.0/version.json

# Release notes
cat versions/1.0.0/RELEASE_NOTES.md
```

## 📝 Creating a New Version

### Step 1: Create Version Directory
```bash
VERSION_NUMBER="X.Y.Z"  # e.g., "1.1.0"
mkdir -p versions/$VERSION_NUMBER
```

### Step 2: Copy Templates
```bash
cp versions/templates/version.json versions/$VERSION_NUMBER/
cp versions/templates/RELEASE_NOTES.md versions/$VERSION_NUMBER/
```

### Step 3: Edit Files
```bash
# Edit metadata
nano versions/$VERSION_NUMBER/version.json

# Edit release notes
nano versions/$VERSION_NUMBER/RELEASE_NOTES.md

# Update changelog
nano CHANGELOG.md

# Update current version
echo "$VERSION_NUMBER" > VERSION
```

### Step 4: Commit and Tag
```bash
git add .
git commit -m "Release version $VERSION_NUMBER"
git tag -a v$VERSION_NUMBER -m "Version $VERSION_NUMBER"
git push origin main --tags
```

## 📚 File Descriptions

| File | Purpose |
|------|---------|
| `VERSION` | Current version number |
| `CHANGELOG.md` | Historical record of all changes |
| `VERSIONING.md` | Complete versioning guide |
| `versions/X.Y.Z/version.json` | Version metadata (structured) |
| `versions/X.Y.Z/RELEASE_NOTES.md` | Version notes (human-readable) |
| `versions/templates/` | Templates for new versions |

## 🏷️ Version Types

| Type | When to Use | Example |
|------|-------------|---------|
| **MAJOR** | Breaking changes | 1.0.0 → 2.0.0 |
| **MINOR** | New features (backward compatible) | 1.0.0 → 1.1.0 |
| **PATCH** | Bug fixes (backward compatible) | 1.0.0 → 1.0.1 |

## 📋 Change Categories

- **Added**: New features
- **Changed**: Changes to existing functionality
- **Deprecated**: Soon-to-be removed features
- **Removed**: Removed features
- **Fixed**: Bug fixes
- **Security**: Security updates

## 🔍 Examples

### Creating Version 1.1.0
```bash
# Create directory
mkdir -p versions/1.1.0

# Copy templates
cp versions/templates/* versions/1.1.0/

# Edit files
nano versions/1.1.0/version.json
nano versions/1.1.0/RELEASE_NOTES.md

# Update VERSION file
echo "1.1.0" > VERSION

# Update CHANGELOG
nano CHANGELOG.md

# Commit
git add .
git commit -m "Release version 1.1.0"
git tag -a v1.1.0 -m "Version 1.1.0"
git push origin main --tags
```

## 📖 Documentation

For more detailed information, see:
- [README.md](README.md) - Overview and getting started
- [VERSIONING.md](VERSIONING.md) - Complete versioning guide
- [versions/README.md](versions/README.md) - Versions directory guide

## ❓ Need Help?

Contact the development team or refer to the documentation files listed above.
