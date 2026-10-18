 Android Forensics Investigation Using SIFT Workstation

Project Overview
A hands-on Android userdata forensic examination using SIFT Workstation, The Sleuth Kit (TSK), SQLite, and ExifTool. The investigation focused on identifying the userdata partition and examining available call-log, contacts, WhatsApp, and image-metadata artifacts.

Tools Used
- SIFT Workstation (Ubuntu)
- The Sleuth Kit: `mmls`
- SQLite
- ExifTool

Investigation Summary
- Identified the userdata partition in `blk0_mmcblk0.bin` using `mmls`.
- Identified an ext4 filesystem at byte offset `3,984,588,800`.
- Mounted the userdata filesystem read-only with journal loading disabled.
- Examined the Android call-log database and documented eight displayed call records.
- Examined the contacts database and correlated the contact entry for “Josh Hickman” with a matching phone number in the call-log records.
- Examined the WhatsApp message database. The database contained 24 message-table records; a small initial sample was reviewed, including text associated with a WhatsApp JID.
- Inspected one JPG with ExifTool. The file had dimensions of 1280 × 853; no capture-time or GPS fields were returned in the examined output. The reported file timestamp must not be treated as the photo's capture time.

Key Findings and Limitations
1. Call-log records and a contact entry shared a matching phone number, providing a correlation within the examined image.
2. WhatsApp database records were present, but only a limited sample was inspected; this project does not claim a complete message-history review.
3. A JPG file was available for metadata examination, but the examined output did not establish capture time or GPS location.
4. Application package directories or MIME-type definitions alone do not prove that a particular user's artifact exists.

 Evidence Handling
- The source image was kept read-only.
- The userdata filesystem was mounted using read-only options with journal replay disabled.
- Do not upload the original device image, private messages, phone numbers, database files, or other potentially sensitive evidence to a public repository.
- Add only sanitized reports and screenshots with personal data redacted.

Repository Contents
- `README.md` — project overview and findings
- `reports/android-forensics-investigation-report.md` — investigation report
- `screenshots/` — add sanitized screenshots of tool output (optional)

## Disclaimer
This project demonstrates a limited educational forensic workflow. Findings should be interpreted in context and independently validated before being used in any real investigation.
