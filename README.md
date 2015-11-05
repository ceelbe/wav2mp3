# wav2mp3
WAV 2 MP3 application

TASK
Write a C/C++ commandline application that encodes a set of WAV files to
MP3
Requirements:
(1) application is called with pathname as argument, e.g.
<applicationname> F:\MyWavCollection all WAV-files contained directly in that folder are to be encoded to MP3
(2) use all available CPU cores for the encoding process in an efficient way by utilizing multi-threading
(3) statically link to lame encoder library
(4) application should be compilable and runnable on Windows and Linux
(5) the resulting MP3 files are to be placed within the same directory as the source WAV files, the filename extension should be changed appropriately to .MP3
(6) non-WAV files in the given folder shall be ignored
(7) multithreading shall be implemented by means of using Posix Threads (there exist implementations for Windows)
(8) the Boost library shall not be used
(9) the LAME encoder should be used with reasonable standard settings (e.g. quality based encoding with quality level "good")

Result:

Linux: 
wav2mp3 -> compiled with gcc/g++ -pthread 4.8.4 from ubuntu14.04 distribution - 
All requirements met (incl. multithreading).

WIN32: wav2mp3.exe -> compiled with gcc/g++ version 4.8.1 from MinGW
1 limitation -> No support for multithreading - I did not manage to compile with  pthreads-w32 library - I'm still looking into this.
All other requirements work.
Tested on folder uploaded as zip file

Files uploaded - needed for compilation:
main.cpp / main.h -> my files
get_audio.c, get_audio.h, congif.h - wrapper for LAME library - These files are adapted from the LAME console application. Reusing 
some helper functions to prepare the WAV file for the encoding (incl. WAV header parsing).
libmp3lame.a - the lame library v3.99.5

Tests: Tested directly using real-life test cases (terminal with wav files in a folder). Due to the easy setup of these tests
no unit test was developed.

Design choices:
Regarding multithreading: I chose a manager-worker approach tackling encoding of several files in parallel - Encoding 1 file 
per thread.
The possible approach of encoding 1 file accross several threads was discarded. The LAME library does not seem to be ready
for this.
Reentrance capability of the library officially supprted by the library. I also made some changes to the lame wrapper to make it
reentrant. 

