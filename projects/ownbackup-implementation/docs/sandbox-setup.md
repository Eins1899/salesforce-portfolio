# OWN Archive — Full Sandbox Setup

## Overview
This document covers the setup and configuration 
of OWN Archive in the RAM Tracking Full Sandbox 
(FullSB) environment.

## Sandbox Details
- Name: FullSB
- URL: ram--fullsb.sandbox.lightning.force.com
- Org ID: 00DAe00000DIRIRMAX
- Type: Full Sandbox

## OWN Archive Package Installation
- Package Name: Own Archive
- Version Installed: 24.32
- Namespace Prefix: OB_Archiver
- Publisher: oarchive
- Installation Date: June 2026
- Installed By: Einstein Amazu

## Installation Steps Followed
1. Located package version from Production 
   Installed Packages
2. Obtained installation link from OWN Support:
   packaging/installPackage.apexp?p0=04tHs000001JewWIAS
3. Constructed Sandbox installation URL:
   https://ram--fullsb.sandbox.lightning.force.com/
   packaging/installPackage.apexp?p0=04tHs000001JewWIAS
4. Installed for All Users
5. Verified in Setup → Installed Packages

## Post-Installation Verification
- Own Archive package visible in Installed 
  Packages ✅
- Archive permission sets visible in 
  Permission Sets ✅
- Archive app visible in App Launcher ✅

## Org Level Settings Enabled
Location: Setup → User Interface
- Set Audit Fields upon Record Creation ✅
- Update Records with Inactive Owners ✅

## Match Production Licenses
- Run via Setup → Company Information → 
  Match Production Licenses
- Completed successfully
- Org ID confirmed: 00DAe00000DIRIRMAX

## OWN Portal Configuration
- Archive service added in app.owndata.com
- Authenticated using dedicated integration user:
  own.archivebackup.integration@ramtracking.com.fullsb
- Service successfully connected ✅

## Archive Policy
- Archive policy configured and tested in Sandbox
- Recovery/unarchive process tested and verified

## Notes
- Production version is 24.24 — Sandbox is 24.32
- Sandbox version is NEWER than Production
- Recommend upgrading Production to 24.32 after 
  testing is complete
- Created: June 2026
- Created by: Einstein Amazu
