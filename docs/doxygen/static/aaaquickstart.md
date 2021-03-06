Quick Start        {#quickstart}
============

[TOC]

If you want to just dive right in and run corsaro on an interface or existing
pcap files, this is the place to start.

Getting Corsaro {#quick_get}
===============

The latest version of Corsaro is
[$(CORSARO_VERSION)](http://www.caida.org/corsaro/downloads/corsaro-2.0.0.tar.gz).

You will also need to have
[libtrace](http://research.wand.net.nz/software/libtrace.php) installed before
building Corsaro (see below for instructions).

Installation {#quick_inst}
============

The following commands will build and install both libtrace and Corsaro into a
custom directory, assuming that the user **does not** have root privileges.

In these examples, we will install everything into `$HOME/corsaro`, meaning that
all Corsaro and libtrace tools will be installed to `$HOME/corsaro/bin`.

### libtrace ###

~~~
tar zxf libtrace-X.X.X.tar.bz2
cd libtrace-X.X.X
./configure --prefix=$HOME/corsaro
make
make install
~~~

### Corsaro ###

~~~
tar zxf corsaro-2.0.0.tar.gz
cd corsaro-2.0.0
./configure CPPFLAGS="-I$HOME/corsaro/include" LDFLAGS="-L$HOME/corsaro/lib"
make
make install
~~~

This will build Corsaro with the \ref plugins_ft plugin only.

For a more detailed description of the configuration options (and to enable more
plugins), see the \ref installation section.  If you require the \ref
plugins_smee plugin, you will need to install the included _libsmee_
library. See the \ref plugins_smee page for more information.

Running Corsaro {#quick_run}
===============

To run the \ref tool_corsaro tool on an existing pcap file to generate \ref
plugins_ft output data, use the following command:

~~~
corsaro -o /path/to/output/file.%P.cors.gz /path/to/pcap/file.pcap.gz
~~~

Replace `/path/to/output/file` with an actual path to the desired output
directory.
Note that the `%%P` is required and will be replaced with a string representing
each component that generates an output file (e.g. `log`, `flowtuple`, etc).

Replace `/path/to/pcap/file` with an actual path to a pcap (or any format
supported by _libtrace_) file.

By default Corsaro will write output data in a compact binary
format where possible. The \ref tool_cors2ascii tool can be used to convert the
binary output files to a human-readable ASCII format.

Running this command will process the given trace file and create four output
files, using the output file template given. Each file will have the `%%P`
replaced with the name of the component that created it.
That is, `global`, `log`, and `flowtuple`.

Corsaro also supports processing packets directly from a live interface. To use
this functionality, replace the pcap file path with:

~~~
pcapint:<interface>
~~~

The \ref tool_corsaro section of this manual contains a more detailed
description of the Corsaro command-line tool.

Viewing the Output {#quick_view}
==================

Once Corsaro has processed the trace file, the resulting data can then be viewed
using the included \ref tool_cors2ascii tool.  Note, the log file is always
written in uncompressed ASCII format, so can be directly viewed using `less`
etc.

To view the \ref plugins_ft output, use the following command:

~~~
cors2ascii /path/to/output/file.flowtuple.cors.gz | less
~~~

This will convert the binary data to a (somewhat) readable ASCII representation.

See the \ref tool_cors2ascii section for a more detailed description of the
tool, and the \ref formats page for a description of the ASCII output.

Further Reading {#quick_further}
===============

This guide provides a very brief description of using Corsaro to analyze trace
data, which should enable you to get started using it quickly.

For more information, take a look through the rest of this manual, starting with
the \ref installation section for practical help getting started, or the \ref
arch section for a description of how the system is designed, and how to extend
it.

