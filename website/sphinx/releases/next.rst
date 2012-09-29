What's new in the next release of Tornado
=========================================

In progress
-----------

* The Tornado test suite now requires ``unittest2`` when run on Python 2.5
  or 2.6.
* `tornado.testing.AsyncTestCase` and friends now extend ``unittest2.TestCase``
  when it is available (and continue to use the standard ``unittest`` module
  when ``unittest2`` is not available)
* `tornado.netutil.bind_sockets` no longer sets ``AI_ADDRCONFIG``; this will
  cause it to bind to both ipv4 and ipv6 more often than before.
* `tornado.netutil.bind_sockets` has a new ``flags`` argument that can
  be used to pass additional flags to ``getaddrinfo``.
* Tornado no longer logs to the root logger.  Details on the new logging
  scheme can be found under the `tornado.log` module.  Note that in some
  cases this will require that you add an explicit logging configuration
  in ordre to see any output (perhaps just calling ``logging.basicConfig()``),
  although both `IOLoop.start()` and `tornado.options.parse_command_line`
  will do this for you.
* Errors while rendering templates no longer log the generated code,
  since the enhanced stack traces (from version 2.1) should make this
  unnecessary.
* `tornado.testing.ExpectLog` can be used as a finer-grained alternative
  to `tornado.testing.LogTrapTestCase`
* The command-line interface to `tornado.testing.main` now supports
  additional arguments from the underlying `unittest` module:
  ``verbose``, ``quiet``, ``failfast``, ``catch``, ``buffer``.
* Empty HTTP request arguments are no longer ignored.  This applies to
  ``HTTPRequest.arguments`` and ``RequestHandler.get_argument[s]``
  in WSGI and non-WSGI modes.
* New function `tornado.testing.bind_unused_port` both chooses a port
  and binds a socket to it, so there is no risk of another process
  using the same port.  ``get_unused_port`` is now deprecated.
* The `tornado.database` module has been removed.  It is now available
  as a separate package, `torndb <https://github.com/bdarnell/torndb>`_
* New class `tornado.iostream.PipeIOStream` provides the IOStream
  interface on pipe file descriptors.
* Much of `IOStream` has been refactored into a separate class
  `BaseIOStream`.
* New class `tornado.process.Subprocess` wraps `subprocess.Popen` with
  `PipeIOStream` access to the child's file descriptors.
