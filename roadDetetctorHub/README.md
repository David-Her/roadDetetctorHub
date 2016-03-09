Libroadfollower
---------------
* CAUTION NEW COMMENT*

README file is underconstruction!!!

---

C++ library for outdoor road navigation.


Compile PC
	mkdir build
	cd build
	cmake ..
	make


Compile for Angstrom (requires complete eldk toolchain + angstrom-omap cmake script):
	mkdir angstrombuild
	cd angstrombuild
	cmake -DCMAKE_TOOLCHAIN_FILE= ../../../rufus-toolchain/cmake_scripts/angstrom-omap.toolchain.cmake ..
	make
