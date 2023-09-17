# Message Digest Algorithm 5 (MD5) Usage

You may have noticed that the engines api returns a string called `md5`, so what is that?

The purpose of using MD5 is to facilitate the comparison between the retrieved engine/package and the one stored on the local device. When a download is initiated, the MD5 checksum of the downloaded package is calculated. This checksum is like a unique fingerprint that represents the content of the downloaded file.

Next, the MD5 checksum of the locally stored package is also computed. By comparing these two MD5 checksums, we can determine if the contents of the downloaded package are identical to those stored on the local device. If the two MD5 checksums are different, it indicates that there is a mismatch between the files, and a download process is triggered to ensure the local copy is updated with the correct version.

## Summary

In summary, MD5 is used as a reliable and efficient way to verify the integrity of files and to decide whether a new download is necessary when dealing with remote packages and local storage.
