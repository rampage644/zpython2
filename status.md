#ZPython 2.7.3 status

##Basic features

No known issues.

##Modules

Modules testing is based on regression tests included in python distribution. 
See available tests in _python-lib-dir/python2.7/test_.

### Production

+ cpickle 
	+ No `statvfs` implementation.
	+ I can't make autotools aware about fake statvfs (nacl-specific toolchain), so just have marked some tests as "Skipped". _Fix_.
+ quopri 
	+ No `popen` implementation.
	+ Better rewrite.
+ random 
	+ No `sleep` implementation.
	+ Better rewrite.
+ argparse 6/1596 failures
+ unicodedata
	+ No `pipe` implementation.

### Experimental

+ posix

	Relies heavily on zrt. Most of features is experimental.

	+ Bunch of `Function not implemented` errors. Have to stub them in glibc to remove from testing or replace with simple implementations.
	+ `chown` not raising `OSError`. Experimental ZRT feature.
	+ stub: lib/zrtlog.c:102: __zrt_log_push_name: Assertion `0' failed
+ os
	+ No `fchdir` implementation.
+ os.path
	+ No `symlink`, `chdir` implementation.
	+ stub: lib/zrtlog.c:102: __zrt_log_push_name: Assertion `0' failed.
+ dummy_threading
	+ No `sleep` support.
	+ Hangs!
+ mmap
	
	Very limited functionality. Almost unsupported feature. 

	+ No large file support 
	+ stub: lib/fs/mem_mount_wraper.cc:480: int mem_close(MountsPublicInterface*, int): Assertion `mnode' failed.

+ hotshot
	+ No `getrusage` implementation.
	+ Again issues with unlinking @tmp (when using -mtest.regrest instead of invoking test_hotshot.py directly)
+ tarfile
	+ No `symlink`, `chdir` implementation.
	+ Filesystem issues (mkdir, unlink, stat)
+ uuid
	+ No `pipe`, `gethostbyname` implementation.
+ import
	+ No `pipe`, `utime` implementation.
	+ Won't import *.pyc files without atime/ctime/utime support.
	+ Can't make skip tests!
+ shutil 
	+ No `mkfifo`, `chdir`, `symlink` implementations.
	+ Segfault!
+ trace 
	+ `rmdir` Not empty, can't remove
	+ failed test 
+ hash 
	+ No `pipe` implementation.
	+ Better rewrite
+ warning
	+ No `pipe` implementation.
	+ Better rewrite
+ sysconfig 
	+ No `symlink` implementation.
+ pkgutil
	+ ZIP does not support timestamps before 1980
+ pydoc
	+ No `pipe` support.
	+ Better rewrite
+ traceback
	+ No `sleep` implementation.
	+ Better rewrite

### Unsupported

* subprocessing
	+ subprocess
	+ popen
	+ popen2
	+ pipes
	+ multiprocessing
	+ commands
	+ asyncore
* GUI
	+ curses
	+ curses.ascii
	+ curses.panel
	+ curses.textpad
	+ Tkinter
	+ Tix
	+ ScrolledText
	+ ttk
	+ turtle
* ZeroVM/Zrt constraints
	+ pdb 
	+ zipfile
	+ signal
	+ ctypes
	+ dl
	+ readline
	+ rlcomleter
	+ ossaudiodev
	+ linuxaudiodev
	+ zipimport
	+ resource
	+ pty
	+ gdb
	+ termios
	+ glob
	+ pwd
	+ select
	+ tty
* networking
	+ mailbox
	+ telnetlib
	+ httpservers
	+ poplib
	+ docxmlrpc
	+ imaplib
	+ ftplib
	+ urllib2
	+ urllib
	+ httplib
	+ socket
	+ smtplib
	+ ssl
	+ mimetools
	+ BaseHTTPServer
	+ CGIHTTPServer
	+ DocXMLRPCServer
	+ SimpleHTTPServer
	+ SimpleXMLRPCServer
	+ SocketServer
	+ smtpd
* MacOS, Windows, IRIX, Sun stuff
	+ aetools
	+ aepack
	+ aetypes
	+ winreg
	+ cd
	+ cl
	+ sv
	+ al
	+ gl
	+ fl
	+ flp
	+ fm
	+ ic
	+ sunaudiodev
	+ winsound
	+ nis
	+ macos
	+ imgfile
	+ msilib
	+ macpath
	+ ntpath
	+ ColorPicker
	+ EasyDialogs
	+ SUNAUDIODEV
	+ FrameWork
	+ MacOS
	+ MiniAEFrame
	+ _winreg
	+ autoGIL
	+ findertools
	+ gensuitmodule
	+ macostools
	+ msvcrt
* Mutithreading
	+ threading
	+ queue
* No compiled modules
	+ bsddb
	+ dbm
	+ gdbm
	+ anydbm
	+ bdb





##Failing regression test list

We've run all tests available under ZeroVM. Test list with brief description follows.

```
# failed or skipped tests for cpython2.7 on zerovm/zrt
# current progress: 144/392 failed tests

io module testing:
# test_largefile # function signal not implemented
# test_fileio # no pipe support, seek issues
# test_file # 99% working, AssertionError: File pos after ftruncate wrong 11 
# test_io # seek/ftruncate issues, no signal, pipe support
# test_grp # unknown error
# test_zipfile64 # test requires loads of disk-space bytes and a long time to run
# test_tempfile.py # no pipe, unlink, remove support
```