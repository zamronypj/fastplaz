Use Of SimpleModel
---

**Simple Query Builder**

example #1

```pascal

  if User
    .Select( '*')
    .Where( 'uname LIKE "%admin%"')
    .OrderBy( 'uid')
    .Limit( 10)
    .Open then
  begin

  end;

```

example #2

```pascal

  if User
    .Select( '*')
    .Where( 'uname = "admin"')
    .OrWhere( 'uname = "agus"')
    .OrderBy( 'uid')
    .Limit( 10)
    .Open then
  begin

  end;

```

example #3

```pascal

  if User
    .Select( '*')
    .Where( 'uid > %d AND uid < %d', [ 5,10])
    .OrderBy( 'uid')
    .Limit( 10)
    .Open then
  begin

  end;

```
