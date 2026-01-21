# Debian 13 Support for LNMP Script

## Changes Made to Support Debian 13 (Trixie)

### 1. Updated OS Detection (`include/check_os.sh`)
- Modified OS version validation to accept Debian versions 9-13
- Updated error message to reflect supported Debian version range

### 2. Updated Package Dependencies (`include/check_sw.sh`)
- Added specific case for Debian 13 with updated package names:
  - `libc-client-dev` instead of `libc-client2007e-dev`
  - `libbz2-dev` instead of `libbz2-1.0`
  - `libncurses-dev` instead of `libncurses5-dev`
  - `libidn12-dev` added for newer IDN library support
  - `libcurl4-openssl-dev` only (removed older `libcurl3-gnutls`)
  - Updated all package names to be compatible with Debian 13

### 3. Updated OpenJDK Installation Scripts
#### `include/openjdk-11.sh`
- Extended Debian 12 special case to include Debian 13
- Uses Adoptium repository for OpenJDK 11 on Debian 13

#### `include/openjdk-17.sh`
- Extended special case to include Debian 13
- Uses Adoptium repository for OpenJDK 17 on Debian 13

#### `include/openjdk-8.sh`
- Already correctly configured (uses else clause for Debian 10+)

### 4. Updated IMAP Extension (`include/pecl_imap.sh`)
- Added conditional logic to use `libc-client-dev` for Debian 13
- Maintains backward compatibility with older Debian versions

## Package Compatibility Changes

### Key Package Updates for Debian 13:
- **libc-client2007e-dev** → **libc-client-dev**
- **libbz2-1.0** → **libbz2-dev**
- **libncurses5/libncurses5-dev** → **libncurses-dev**
- Added **libidn12-dev** for updated IDN library
- Removed **libcurl3-gnutls** (deprecated in newer Debian)
- Updated several development libraries to their current naming conventions

## Testing

All modified scripts have been syntax-checked and should work correctly with:
- OpenResty installation (latest version)
- All OpenJDK versions (8, 11, 17)
- PHP extensions including IMAP
- All LNMP stack components

## Installation Command

To install OpenResty on Debian 13:
```bash
./install.sh --nginx_option 3
```

This will install OpenResty (option 3) with all the updated dependencies for Debian 13 compatibility.