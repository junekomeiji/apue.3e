Read the file called DISCLAIMER.

On Freebsd, type "gmake".
On other platforms, type "make" (as long as this is gnu make).

For FAQs, updated source code, and the lost chapter, see http://www.apuebook.com.
Please direct questions, suggestions, and bug reports to sar@apuebook.com.

Steve Rago\
January 2013

--------------------------------------------------------------------------------
This repository has taken several years off my life span. After spending a whole
day searching down random Stack Exchange questions, as well as fiddling around 
with gcc and the code itself, I have finally gotten it to compile. I haven't
tested anything in the repository yet, though I will soon.

I have made various changes to various parts of the codebase. So far, here is
what I've changed:

in `./db/Makefile`:\
`else
  LDCMD=$(CC) -shared -Wl,-dylib -o libapue_db.so.1 -L$(ROOT)/lib -lapue -lc db.o`\
becomes\
`else
  LDCMD=$(CC) -shared -o libapue_db.so.1 -L$(ROOT)/lib -lapue -lc db.o`
 
I'm not sure why my computer keep spitting out that there's disambiguity with the
argument of -dylib, and the only other piece of documentation seems to be a 
Chinese BBS for the Beijing University of Posts and Telecommunications which
requires me to sign in for an account. Not wanting to do that, I simply removed
the -Wl,dylib argument for the linker and everything seemed to work fine. 

The next thing that I had to alter was in `./filedir/devrdev.c` where I added:

`#ifdef LINUX
#include <sys/sysmacros.h>
#endif`

because `major()` and `minor()` were not imported for some reason. Maybe it is on other
UNIXes, but I doubt Linux comes with `major()` and `minor()` just hanging about for no
reason.

The last change that I did was in `./stdio/buf.c`.
Full credit to the solution goes to JinshengStatham who provided a
working solution to the problem, and it seems to come from the non-portability of 
the code itself.

https://stackoverflow.com/questions/55770771/how-to-fix-struct-file-has-no-member-named-pad-error-when-using-make-in

Rago's book is a very good resource for learning about the core intricacies of UNIX. 
However, the fact that the book's source code has gone unmaintained and doesn't 
compile on its own without quite some bit of assistance shows that it's probably time
for a fourth edition to come out.

This repository solely exists to prevent myself from accidentally deleting all 
my work on accident, and I make no guarantees on how well this repository of
arcane UNIX functions will run on your system.

May God be with you.

June Komeiji\
October 2022
