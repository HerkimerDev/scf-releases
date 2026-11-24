# scf-mirror

Release zips of [Secure Custom Fields](https://wordpress.org/plugins/secure-custom-fields/)
(SCF), copied from wordpress.org.

This is for WordPress sites on a host that cannot download plugins from
wordpress.org. The official GitHub repo `WordPress/secure-custom-fields`
stopped attaching zips to its releases at 6.9.9.

## How it works

`.github/workflows/mirror.yml` runs every 6 hours, and when started by hand:

1. It gets the latest SCF version from the wordpress.org plugin API.
2. If this repo already has a release with that tag, it stops.
3. It downloads the official zip from `downloads.wordpress.org`.
4. It compares each file in the zip with the official wordpress.org checksums
   for that version (`downloads.wordpress.org/plugin-checksums/`). If a file
   is different, missing or extra, the job fails and publishes nothing.
5. It publishes a release with the tag `<version>` and the unchanged zip as the
   asset `secure-custom-fields.zip`.

The zip is the file from wordpress.org, byte for byte. Nothing in this repo
changes it.
