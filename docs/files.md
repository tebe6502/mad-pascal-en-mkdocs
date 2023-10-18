# File operations

## [FILE](http://localhost:8000/typy/#plikowe-binarne)

```delphi
var f: file;
```

## [TEXT](http://localhost:8000/typy/#plikowe-tekstowe)

```delphi
var f: text;            // TEXT
    g: textfile;        // TEXTFILE alternatively
```


## [ASSIGN](http://localhost:8000/biblioteki-podstawowe/#assign)


Example of channel opening for **S:** device (screen) to output characters in `GRAPHICS 1`, `GRAPHICS 2` mode
```delphi
var scr: text;
    s: string = 'color COLOR ' + #155 + 'COLOR '* + 'color '*;

begin

 assign(scr, 'S:');      // before InitGraph
 rewrite(scr);           // before InitGraph

 InitGraph(2);           // Graphics 2
 
 GotoXY(1,6);
 
 write(scr, s);

 close(scr);

end.
```

## [RESET](http://localhost:8000/biblioteki-podstawowe/#reset)

```delphi
var t: text;

 reset(t);          // for reading a text file, no additional parameter with record size
```

```delphi
var f: file;

 reset(t, 1);       // for reading a binary file (record = 1)
```

If no record length is specified for the binary file `FILE`, the default value =128 will be taken

## [REWRITE](http://localhost:8000/biblioteki-podstawowe/#rewrite)

```delphi
var t: text;

 rewrite(t);        // for writing a text file, no additional parameter with record size
```

```delphi
var f: file;

 rewrite(f, 1);     // for writing a binary file (record = 1)
```

If no record length is specified for the binary file `FILE`, the default value =128 will be taken


## [APPEND](http://localhost:8000/biblioteki-podstawowe/#append)

```delphi
var
 t: text;

begin

 assign(t, 'D:TEXT.TXT');
 append(t);

 writeln(t, 'ATARI');

 writeln(t, 'C64');

 write(t, 'Amstrad');

 close(t);
```


## [BLOCKREAD](http://localhost:8000/biblioteki-podstawowe/#blockread)

```delphi
var f: file;
    pnt: pointer;

begin

 pnt:=pointer(dpeek(88));

 assign(f, 'D:FILENAME');
 reset(f, 1);
 blockread(f, pnt^, 8);
 close(f);

end.
```


```delphi
var f: file;
    buf: array [0..0] of byte;

begin

 buf:=pointer(dpeek(88));

 assign(f, 'D:FILENAME');
 reset(f, 1);
 
 blockread(f, buf, 8);
 close(f);

end.
```

## [BLOCKWRITE](http://localhost:8000/biblioteki-podstawowe/#blockwrite)

```delphi
var f: file;
    buf: array [0..0] of byte ABSOLUTE $bc40;

begin

 assign(f, 'D:FILENAME');
 rewrite(f, 1);
 
 blockwrite(f, buf, 40*24);
 close(f);

end.
```
