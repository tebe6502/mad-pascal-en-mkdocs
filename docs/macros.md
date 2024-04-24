#

## [Macros](https://www.freepascal.org/docs-html/prog/progse5.html)

**Mad-Pascal** allows you to use macros, just like **FPC**, except that macros are always enabled.

```delphi
 {$macro on}
 {$macro off}
 {$macro+}
 {$macro-} 
```

The `{$macro on}` directive is required by **FPC**, in **Mad-Pascal** it is retained for compatibility purposes only.

### Defining a macro

```delphi
{$define label := expression}

{$define label(par0, par1 ... par7) := expression}
```

For a definition to be recognized as a macro, the assignment symbol `:=` must occur after the label name and any `(par0..par7)` parameter list.


```delphi
{$define new_proc :=

procedure test;
begin

 writeln('ok');

end;
}


  new_proc


begin

 test;

end.
```

```delphi
{$define sum_xi

 :=

 x:=x+i;
 }
 
begin

 sum_xi;
 
end;
```

```delphi
{$define WIDTH := 80}
{$define LEN   :=   ( WIDTH + 10 )}

var a: byte;

begin

 a := len * 20;

end.
```

Macros with parameters are supported by **Mad-Pascal** but not by **FPC**, keep this in mind if you intend to test code on other hardware platforms.

```delphi
{$define SIGN_MASK := $8000}
{$define SIGNED_INF_VALUE(x) := ((x and SIGN_MASK) or $7C00)}

var a: byte = 11;

begin

 writeln( SIGNED_INF_VALUE(a shl 15) );

end.
```
