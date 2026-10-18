 Android Forensics Investigation Report

1. Objective
Examine an Android userdata filesystem image in a controlled lab environment and identify selected artifacts relevant to mobile-device forensics.

2. Evidence and Environment
- Evidence image: `blk0_mmcblk0.bin`
- Analysis environment: SIFT Workstation (Ubuntu)
- Filesystem: ext4
- Userdata partition start sector: `7,782,400`
- Sector size: `512 bytes`
- Partition byte offset: `3,984,588,800`
- Mount approach: read-only, with ext4 journal loading disabled (`ro,noload`)

The original evidence image was not intentionally modified during this examination.

3. Tools
- The Sleuth Kit (`mmls`)
- SQLite
- ExifTool

4. Examination and Results

4.1 Partition and Filesystem
`mmls` was used to inspect the partition layout. The userdata partition was identified starting at sector 7,782,400. `blkid` identified an ext4 filesystem at the corresponding byte offset.

4.2 Call Logs
The database `data/com.android.providers.contacts/databases/calllog.db` contained a `calls` table. Eight displayed records were reviewed.

The displayed records included several entries associated with the number `9102697333` and the saved name “Josh Hickman”, along with other entries. Standard Android call-type values were interpreted as outgoing (`2`) and missed (`3`). A zero duration alone was not treated as proof that a call connected or failed.

SHA-256 of the examined `calllog.db`:
`b6e3d2a2484e8be89489d88d58ea763199bcbe870c58f670f42ff78b661e142b`

4.3 Contacts
The separate `contacts2.db` database contained a contact record for “Josh Hickman” and a phone number formatted as `(910) 269-7333`. Its digits matched the number seen in the call-log records.

This is a correlation between records in the examined image; it is not independent verification of a real-world person's identity.

4.4 WhatsApp
The WhatsApp `msgstore.db` database contained a `messages` table with 24 records in total. A limited initial sample was inspected. The sample included entries associated with `19102697333@s.whatsapp.net`, including the text “What's up?!?!“ and a received message reading “Hey man! What's happening? Welcome to WhatsApp!”

 
4.5 Image Metadata
ExifTool was used to inspect:
`data/media/0/DCIM/C79D9FD1-C3A3-4BBB-BD52-0CAEA0E4DF48-1.jpg`

The examined output reported JPEG format, approximately 150 kB, and dimensions of 1280 × 853 pixels. The output did not provide a capture-time or GPS field. A file modification timestamp is not equivalent to the original capture time.

5. Conclusions
This exercise demonstrated a basic Android userdata examination workflow: partition identification, read-only filesystem access, SQLite artifact review, cross-database correlation, and image metadata inspection.

 

 
