## Sommaire

1. [Utilisation de base](#utilisation-de-base)
2. [Utilisation avancée](#utilisation-avancee)
3. [FAQ](#faq)

# 1. Utilisation de base
<span id="utilisation-de-base"></span>

# 2. Utilisation avancée
<span id="utilisation-avancee"></span>

# 3. FAQ
<span id="faq"></span>
# Add to Archive Dialog Box

Allows you to specify options for creating or updating an archive.

#### How to call this dialog box

1. In Windows Explorer or in 7-Zip, right-click the file(s) or folder(s) you want to compress.
2. Point to **7-Zip**, and then click the **Add to archive...** command item.

#### Parameters

Some compression options fields have an option item with an asterisk (*). This is the default value. And it is recommended to use this default option value with an asterisk (*).

Archive

Provides a space for you to specify a destination archive name. You can click "**...**" button to display "Open" dialog box that you can use to locate archive.

Archive format

Specifies a format of created archive. Some formats (gzip and bzip2) do not support compressing more the one file per archive.

Compression level

Specifies compression level. There are 6 levels of compression:

|Value|Meaning|
|---|---|
|0 - Store|Files will be copied to archive without compression.|
|1 - Fastest|Fastest compression.|
|3 - Fast|Fast compression.|
|5 - Normal|Compression with balanced settings.|
|7 - Maximum|Can give a higher compression ratio than Normal level. But it can be slower, and it can require more memory.|
|9 - Ultra|Can give a higher compression ratio than Maximum level. But it can be slower, and it can require more memory.|

Compression method

Specifies compression method. Each archive format can have its own compression methods:

|Method|Description|
|---|---|
|LZMA|It's base compression method for 7z format. Even old versions of 7-Zip can decompress archives created with LZMA method. It provides high compression ratio and very fast decompression.|
|LZMA2|Default compression method of 7z format. LZMA2 is LZMA-based compression method. It provides better multithreading support than LZMA. But compression ratio can be worse in some cases. For best compression ratio with LZMA2 use 1 or 2 CPU threads. If you use LZMA2 with more than 2 threads, 7-zip splits data to chunks and compresses these chunks independently (2 threads per each chunk).|
|PPMd|Dmitry Shkarin's PPMdH algorithm with small changes. Usually it provides high compression ratio and high speed for text files.|
|BZip2|Standard compression method based on BWT algorithm. Usually it provides high speed and pretty good compression ratio for text files.|
|Deflate|Standard compression method of ZIP and GZip formats. Compression ratio is not too high. But it provides pretty fast compressing and decompressing. Deflate method supports only 32 KB dictionary.|
|Deflate64|Modified version of Deflate algorithm with bigger dictionary (64KB).|

Dictionary size

Specifies Dictionary size for compression method.

Usually, a higher Dictionary size gives a higher compression ratio. But compressing can be slower and it can require more memory.

Memory (RAM) usage for LZMA compressing is about 11 times the dictionary size. Memory usage for LZMA decompressing is close to value of dictionary size.

Memory (RAM) usage for LZMA2 compressing / decompressing depends on the dictionary size and the number of CPU threads used by the LZMA2 encoder and LZMA2 decoder.

Memory usage for PPMd compressing and decompressing is almost equal to dictionary size.

Word size

Specifies the length of words, which will be used to find identical sequences of bytes for compression.

Usually for LZMA and Deflate, big Word size gives a little bit better compression ratio and slower compression process. A big Word size parameter can significantly increase compression ratio for files which contain long identical sequences of bytes. For PPMd, the Word size strongly affects both compression ratio and compression/decompression speed.

Solid Block size

Specifies the size of a solid block. You can also disable solid mode. In solid mode all files will be compressed as continuous data blocks. Usually compressing to a solid archive improves the compression ratio. You can use this option only for 7z archives. The updating of solid .7z archives can be slow, since it can require some recompression.

Number of CPU threads

Specifies the number of threads for compressing. A big number of threads can speed up compression speed on Multi-Processor systems. Sometimes it can increase speed even on single-core CPU.

Memory usage for Compressing

Specifies the amount of memory (RAM) that is allowed to be used for compression.

There is an additional information line, that shows 3 numbers:

Example: 4669 MB / 26 GB / 32 GB:

- value 1 : 4669 MB : the expected amount of memory that 7-Zip will use, based on other compression settings. In the example: 7-Zip will use up to 4669 MB for the following compression settings: LZMA2 compression method, 64MB dictionary size, 8 CPU threads.
- value 2 : 26 GB : memory usage limit set by the "Memory usage for Compressing" option. 7-zip will check that the actual memory usage (value 1) doesn't exceed the user-set limit (value 2).
- value 3 : 32 GB : the total size of RAM memory in computer. It is recommended that the user-set limit (value 2) be less than the RAM size (value 3).

The default value for "Memory usage for Compressing" option is "* 80%". This means that 7-Zip is allowed to use up to "80%" of the total RAM size, for example, 26 GB usage that is 80% from 32 GB (RAM Size). But the actual memory usage depends on other settings: "Compression method", "Dictionary size" and "Number of CPU threads".

Note: High memory usage, close to or greater than the total RAM size, can make the compression process several times slower than normal processing, since the system may use slow swapping of memory pages between RAM and storage. If the expected amount of memory that 7-Zip will use exceeds the user-set limit, 7-Zip will not start compression and will display an error message. It protects the user from selecting settings that may slow down the system.

Note: If the option "Number of CPU threads" is set to the default value with asterisk (*), changing the "Memory usage for Compressing" option may change the number of CPU threads that will be used for compression.

Memory usage for Decompressing

Shows the amount of memory (RAM) required for decompression according to the selected compression settings.

It shows the minimum amount required. But the actual memory usage for decompression may be higher than the shown value, because 7-Zip can use additional memory for decompression if the RAM size allows it. This extra memory can be used to increase the decompression speed with additional CPU threads. Note: 7-Zip doesn't use additional memory for decompression that exceeds 55% of the computer's RAM that will be used for decompression.

Split to volumes

    {Size}[b | k | m | g]
    

Specifies volume sizes in Bytes, Kilobytes (1 Kilobyte = 1024 bytes), Megabytes (1 Megabyte = 1024 Kilobytes) or Gigabytes (1 Gigabyte = 1024 Megabytes). If you specify only {Size}, 7-zip will treat it as bytes. It's possible to specify several values. Example:

    10k 15k 2m
    

The first volume will be 10 KB, the second will be 15 KB, and all others will be 2 MB.

Parameters

Allows you to specify parameters for compression. See the [-m (Method)](../../../../cmdline/switches/method.htm) switch description for more details. It's allowed to omit the -m prefix (as in -m switch) when using this dialog box.

**Examples**

      f=delta:4
      -mf=delta:4

uses Delta:4 filter (if you want to compress WAV files).

      f=bcj2
      -mf=bcj2

uses BCJ2 filter (for x86 executables).

Update mode

Specifies update mode:

|Value|Meaning|
|---|---|
|Add and replace files|Add all specified files to the archive.|
|Update and add files|Update older files in the archive and add files that are new to the archive.|
|Freshen existing files|Update specified files in the archive that are older than the selected disk files.|
|Synchronize files|Replace specified files only if added files are newer. Always add those files, which are not present in the archive. Delete from archive those files, which are not present on the disk.|

Path mode

Specifies how path names will be stored in archive:

|Value|Meaning|
|---|---|
|Relative pathnames|Store file paths relative to current folder.|
|Full pathnames|Store file paths relative to root of the volume, excluding volume name prefix.|
|Absolute pathnames|Store fully qualified file paths including volume name.|

Options

Specifies compression options:

|Option|Meaning|
|---|---|
|Create SFX archive|Create self-extracting archive. You can use this option only for 7z archives. Look to [-sfx (Create SFX archive)](../../../../cmdline/switches/sfx.htm) switch description for more details about SFX modules.|
|Compress shared files|Compress files open for writing by another applications.|
|Delete files after compression|Delete files after including to archive. So it works like moving files to archive. 7-Zip deletes files at the end of operation and only if archive was successfully created.|

Encryption

Specifies password and encryption options.

Enter password

Specify password here

Reenter password

Reenter password here for verification

Show Password

Shows Password

Encryption method

Specifies the encryption method. For 7z format, it can be only AES-256. For ZIP format you can select ZipCrypto or AES-256. Use ZipCrypto, if you want to get archive compatible with most of the ZIP archivers. AES-256 provides stronger encryption, but now AES-256 is supported only by 7-Zip, WinZip and some other ZIP archivers.

Encrypt file names

Enables or disables archive header encryption, including file name encryption.

Options : button

Opens another window with additional options. It allows you to specify what timestamps will be stored to the archive. Also for some archive formats (wim and tar) it allows you to specify options for storing hard links and symbolic links. And for wim format it allows you to specify options for storing alternate data streams and file security information.

There are two checkboxes for each "store time" option. If you set first checkbox, it will allow you to change the second checkbox. If the second checkbox is set, 7-zip stores the corresponding timestamps to the archive. If the second checkbox is not set, 7-zip doesn't store the corresponding timestamps to the archive. If you don't set first checkbox, 7-Zip uses default value for second checkbox. Default values for timestamp storing are the following: store only "modification time" to the archive, and not store "last access time" and "creation time".

| Option                                      | Meaning                                                                                                                                                               |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Store symbolic links                        | Store symbolic links as symbolic links in archive.                                                                                                                    |
| Store hard links                            | Store hard links as hard links in archive.                                                                                                                            |
| Store alternate data streams                | Store alternate data streams in archive.                                                                                                                              |
| Store file security                         | Store file security records in archive.                                                                                                                               |
| Timestamp precision                         | Set format of timestamp precision for storing in archive. It can be selected from the following options: 100 ns (Windows), 1 ns (Linux), 1 sec (Unix) or 2 sec (DOS). |
| Store modification time                     | Store files modification time in archive.                                                                                                                             |
| Store creation time                         | Store files creation time in archive.                                                                                                                                 |
| Store last access time                      | Store files last access time in archive.                                                                                                                              |
| Set archive time to latest file time        | If the checkbox is switched on, 7-Zip sets timestamp for archive file as timestamp from the most recently modified file in that archive.                              |
| Do not change source files last access time | If the checkbox is switched on, 7-Zip doesn't allow the system to change "last access time" property of source files during archiving operation.                      |
