#

## [Resource files](/syntax/#r-resource)

### Syntax of RC files

The `RC` files are plain text files. They contain a list of resources to be included in the compiled file.
The basic syntax element looks as follows:

	RCLABEL      RCTYPE     RCFILE      [PAR0, PAR1, PAR2, PAR3, PAR4, PAR5, PAR6, PAR7]

The contents of a `RC` file may include comments, preceded by a ';' or '#' character. An example of a `RC` file:

	; this is a MPT player
	mpt_player	MPTPLAY
	
	# this is a MPT modul
	mpt_modul	MPT	'porazka.mpt'

The resource type specifies the format of the file to be included.

| Type       | Info                                                                                                   |
|:----------:|--------------------------------------------------------------------------------------------------------|
| RCDATA     | Any data type, e.g.:                                                                                   |
|            | label RCDATA 'filename'                                                                                |
|            | label RCDATA 'filename' OFFSET                                                                         |
| EXTMEM     | Any data type loaded into **PORTB** secondary memory, loading address determined by `RCLABEL`.         |
| RCASM      | The assembler file that will be included and assembled.                                                |
| DOSFILE    | File with **Atari DOS** header, the loading address of such a file should be identical to `RCLABEL`.   |
| RELOC      | Relocatable file in **Mad-Assembler** format, the file will be relocated to the indicated `RCLABEL` address.|
| RMT        | The **Raster Music Tracker-a** module file, the file will be relocated to the indicated `RCLABEL` address.  |
| MPT        | The **Music ProTracker-a** module file, the file will be relocated to the indicated `RCLABEL` address.      |
| CMC        | The **Chaos Music Composer-a** module file, the file will be relocated to the indicated `RCLABEL` address.  |
| SAPR       | **SAP-R** data file, the file will be relocated to the indicated `RCLABEL` address.                    |
| RMTPLAY    | Player for **RMT** module, specify *.FEAT file as `RCFILE` and additionally `PAR0` player mode 0..3:        |
|            | 0 => compile RMTplayer for 4 tracks mono                                                               |
|            | 1 => compile RMTplayer for 8 tracks stereo                                                             |
|            | 2 => compile RMTplayer for 4 tracks stereo L1 R2 R3 L4                                                 |
|            | 3 => compile RMTplayer for 4 tracks stereo L1 L2 R3 R4                                                 |
| SAPRPLAY   | Player **SAP-R LZSS**, no need to specify file name `RCFILE`, address `RCLABEL` only from the beginning of the page. |
| MPTPLAY    | Player for **MPT** module, no need to specify `RCFILE` file name.                                      | 
| CMCPLAY    | Player for **CMC** module, no need to specify `RCFILE` file name.                                      |
| XBMP       | Windows Bitmap** file (8 BitsPerPixel) loaded into **VBXE** memory at the indicated `RCLABEL` address from color index `PAR0` in **VBXE** color palette #1 |

&nbsp;
### Ability to load resources under ROM

        CMC             RAM / ROM
        CMCPLAY         RAM / ROM
        DOSFILE         RAM / ROM
        EXTMEM
        MPT             RAM / ROM
        MPTPLAY         RAM / ROM
        RCASM           RAM / ROM
        RCDATA          RAM / ROM
        RELOC           RAM
        RMT             RAM / ROM
        RMTPLAY         RAM
        XBMP
        SAPR            RAM / ROM
        SAPRPLAY        RAM / ROM

### Including an RC file in the application

Insert a compiler directive in the program source code (e.g., at the beginning of the implementation section):

	{$R myresources.rc}

In addition, specify in the program code the value for the `RCLABEL` labels of the corresponding resources, e.g.:

```delphi
const

    mpt_player = $8000;

    mpt_modul = $9000;
```

The inclusion of the `RC` file occurs when the program is compiled.

If the resource address points to an address under ``ROM`` (``$C000..$FFFF``) then ``ANTIC`` is disabled. At program startup, write the appropriate value to the ``DMACTL`` registry.
to turn the image back on.

### Access to Resources

Resources are placed at the indicated `RCLABEL` addresses in memory. The only exception is the `RCDATA` resource type for which it is possible to omit the `RCLABEL` definition from the program code.

In the absence of a `RCLABEL` definition, the resource is included in the compiled program, accessed via the `GetResourceHandle` routine.

	GetResourceHandle(pointer, 'rclabel');

The `GetResourceHandle` procedure sets the value of the POINTER for the resource 'RCLABEL'.
