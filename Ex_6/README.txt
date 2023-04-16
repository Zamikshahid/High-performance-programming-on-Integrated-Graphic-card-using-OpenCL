1. Install freeglut MSVS package for 64 and x86 :
	https://www.transmissionzero.co.uk/files/software/development/GLUT/freeglut-MSVC.zip
2. Install glew binaries for Windows x86 and 64: 
	https://sourceforge.net/projects/glew/files/glew/2.1.0/glew-2.1.0-win32.zip/download
3. After one compilation of cmake it will show errors with freeglut.dll and glew.dll
	To solve it copy freeglut.lib and glew32.lib files into the "out/build/Release"  and  "out/build/Debug" folders. 
	In case you delete the Cmake cache you should repeat the step3
4. The file freeglut.lib can be found from the folder you will extract in step1 in the path "freeglut\lib\x64\freeglut.lib"
	The file glew.lib will be taken from the folder to which you will extract the file in step 2 in the path :C:\glew-2.1.0\lib\Release\x64\glew32.lib