[![Actions Status](https://github.com/lizmat/HTTP-Status/workflows/test/badge.svg)](https://github.com/lizmat/HTTP-Status/actions)

NAME
====

HTTP::Status - Information about HTTP Status Codes

SYNOPSIS
========

```raku
use HTTP::Status;

say HTTP::Status(200);          # OK

say HTTP::Status(200).title;    # OK

say HTTP::Status(200).type;     # Success

say HTTP::Status(200).summary;  # Standard response for successful HTTP...

say HTTP::Status(200).origin;   # IANA

say HTTP::Status(200).since;    # HTTP/1.0

say HTTP::Status(200).RFC;      # 7231

say HTTP::Status(200).code;     # 200

say HTTP::Status.source;        # https://en.wikipedia.org/....

# Legacy interface
say get_http_status_msg(200);   # OK

say "Informational" if is-info($code);
say "Success" if is-success($code);
say "Redirection" if is-redirect($code):
say "Error" if  is-error($code);
say "Client Error" if is-client-error($code);
say "Server Error: if is-server-error($code);
```

DESCRIPTION
===========

The `HTTP::Status` class contains information about HTTP Status Codes as can be found on [Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).

To obtain the information about a given HTTP Status Code, one calls the `HTTP::Status` class with the code in question:

```raku
my $status = HTTP::Status(200);
```

This returns **the** `HTTP::Status` object for the given code, or it returns `Nil` if the code is unknown.

The `HTTP::Status` object stringifies to its `title`, and numifies to its `code`:

```raku
say $status;   # OK

say +$status;  # 200
```

It also contains the type of status code and a summary of additional information about that status code that may be useful as a further help in debugging issues:

```raku
say $status.type;     # Success

say $status.summary;  # Standard response for successful...
```

Apart from `title`, `type`, `code` and `summary`, the object also contains information about the applicable `RFC`, its `origin` and `since` which version of the HTTP protocol it has been available:

```raku
say $status.origin;  # IANA

say $status.RFC;     # 7231

say $status.since;   # HTTP/1.0
```

LEGACY INTERFACE
================

The legacy interface is identical to the version originally created by `Timothy Totten`.

get_http_status_msg
-------------------

Returns the string for the given HTTP Status code, or `Unknown`.

is-info
-------

Returns whether the given HTTP Status code is informational (100..199).

is-success
----------

Returns whether the given HTTP Status code indicates success (200..299).

is-redirect
-----------

Returns whether the given HTTP Status code indicates a redirection of some kind (300..399).

is-error
--------

Returns whether the given HTTP Status code indicates a some kind of error (400..599).

is-client-error
---------------

Returns whether the given HTTP Status code indicates a some kind of client error (400..499).

is-server-error
---------------

Returns whether the given HTTP Status code indicates a some kind of server error (500..599).

ADAPTING INFORMATION
====================

If you want to add or adapt the information as provided by this class, you can easily do that by creating a new `HTTP::Status` object in sink context.

```raku
HTTP::Status.new(
  code    => 666,
  title   => "Too Evil",
  summary => "That is really not allowed!",
  origin  => "Hell",
  since   => "HTTP/6.0",
  RFC     => 6666,
);

say HTTP::Status(666);  # Too Evil
```

COPYRIGHT AND LICENSE
=====================

Copyright 2012-2020 Timothy Totten

Copyright 2021 Elizabeth Mattijsen

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

