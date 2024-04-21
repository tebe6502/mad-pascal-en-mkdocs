# Alternative to DOS

## [foxDOS](https://github.com/tebe6502/Mad-Assembler/blob/master/examples/foxdos.asm)

* installs the D: device like any other DOS Atari
* loads a bootable file named AUTORUN at startup
* supports the standard DOS 2 file system
* the supported sector size (128 or 256 bytes) is determined at the foxDOS compilation stage
* foxDOS allows a file to be read by D:
* supports BINARY LOAD function, e.g. XIO 40,#1,0,0, "D:FILE.EXE"
* foxDOS fits entirely into pre-read sectors (boot sectors)
* foxDOS does not set MEMLO, but only occupies the memory area $0700..$097F
* foxDOS does not disable the ROM during transmission

limitations:

* only one file can be read at a time, but it can be of any length
* allows overwriting an existing file that fits in only one sector
* other operations such as reading a directory, deleting, renaming, etc. are not supported

```
copy filename.obx disk\autorun.

dir2atr.exe -md -B foxdos.obx disk.atr disk\ 
```

## [xBootDOS](https://xxl.atari.pl/xbootdos/)

* MEMLO = $980, does not use $04xx,$05xx or $06x page
* after loading, it automatically runs the program stored under the name "AUTO"
* automatically configures itself to the appropriate sector size (128/256) of SD/ED/DD and DOS2 file system version (disk image size up to 16 MB)
* also supports BiboDOS and TopDOS systems with 64/128 directory entries
* allows you to overwrite existing files
* supports BINARY LOAD function, e.g. XIO 40,#1,0,0, "D:FILE.EXE"
* additional NOTE and POINT commands are included in the xBDext file (can be loaded automatically - rename to AUTO)

limitations:

* only one file can be read at a time, but it can be of any length
* other operations such as reading a directory, deleting, renaming, etc. are not supported

```
copy filename.obx disk\autorun.

dir2atr.exe -md -B xBootDOS.obx disk.atr disk\ 
```

## [dir2atr](https://www.horus.com/~hias/atari/)

A program for **Windows** with which you can create floppy disk images **Atari 8-Bit** `ATR`
