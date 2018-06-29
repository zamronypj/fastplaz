
FastPlaz
===


Package
---
* fastplaz_cms.lpk


## USER UTILS USAGE
---

initialization
```
  UsersUtil := TUsersUtil.Create();
```
or with this statement
```
  with TUsersUtil.Create() do
  begin
  .
  .
  .
  end;
```

optional :
```
  UsersUtil.LoginAttempsMax := 3; // default = 0
  UsersUtil.OnLoginAttemps := @LoginAttemps; // callback, if too many login attempts
```

check is loggedin or not
```
  if UsersUtil.isLoggedIn then
  begin
    ....
  end
```

login with username & password
```
  if UsersUtil.Login( 'theusername', 'thepassword') then
  begin
  ....
  end;
```

add user
```
  lastUserID := UsersUtil.Add( 'theusername', 'theusername@email.com', 'password');

  // or, with random password

  lastUserID := UsersUtil.Add( 'theusername', 'theusername@email.com');
```

add user with params
```
  params := TStringList.Create;
  params.Values['activated'] := '1';
  params.Values['approved_by'] := '0';
  lastUserID := UsersUtil.Add( 'theusername', 'theusername@email.com', '', params);
```

assign user to group
```
  UsersUtil.AssignToGroup( 24, 1);

  UsersUtil.AssignToGroup( 24, 'Users');
```

change password
```
  UsersUtil.ChangePassword( 3, 'newpassword');
```

## GROUP UTILS USAGE
---

add group
```
  with TGroupsUtil.Create() do
  begin
    Add( 'groupname', 'group description', GROUP_TYPE_PUBLIC)
    ;
  end;
```

add user to group
```
  TGroupsUtil.AddUserToGroup( 1, 'Users');

  // or

  TGroupsUtil.AddUserToGroup( 1, 1);
```

## PERMISSION UTILS
---

check permission
```
   with TPermissionUtil.Create() do
   begin
     if checkPermission( 'modulename', 'instance', ACCESS_DELETE, UserId) then
     begin
     .
     .
     .
     end;
     Free;
   end;
```

other way to check permission from existing loggedin user
```
  if UsersUtil.checkPermission( 'modulename', 'instance', ACCESS_DELETE) then
  begin
  .
  .
  .
  end;
```

get security level
```
  userID := 2;
  secLevel := getSecurityLevel( userID, 'modulname', 'list');
```

get security level from any instance
```
  userID := 2;
  secLevel := getSecurityLevel( userID, 'modulname', 'any');
```

## FORM SECURITY
---

CSRF
```
  if isPost then
  begin
    if not isValidCSRF then
    begin
      ThemeUtil.FlashMessages:= 'Security: Invalid CSRF Token';
      Redirect( BaseURL);
    end;
  end;
```

in HTML layout, just add this :
```
  <form id="user_login" class="" action="" method="post">
    [csrf-token name="optionalmodulename"]

    ...
    ...
    <input id="someid" type="text" name="somename" >
    <input id="someid2" type="text" name="somename2" >
    ...
    ...

  </form>
```
example result:
```
  <form id="user_login" class="" action="" method="post">
    <input type="hidden" name="csrftoken" value="mFqiGVTovWl3" id="FormCsrfToken_optionalmodulename" />

    ...
    ...
```

