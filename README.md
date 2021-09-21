# Steps to install GNU GCC on Mac

* Install `brew` tool from [here](https://brew.sh)
* Run following commands to install GNU GCC:
```
brew update
brew upgrade
brew info gcc
brew install gcc
brew cleanup
```
* Once installed, run `brew info gcc` to see the location of install and identify the g++ binary name (Eg: `g++-11`). Example:
```
$ brew info gcc
gcc: stable 11.2.0 (bottled), HEAD
GNU compiler collection
https://gcc.gnu.org/
/opt/homebrew/Cellar/gcc/11.2.0 (1,412 files, 339.5MB) *
  Poured from bottle on ....
From: https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/gcc.rb
License: GPL-3.0-or-later with GCC-exception-3.1
==> Dependencies
Required: gmp ✔, isl ✔, libmpc ✔, mpfr ✔, zstd ✔
==> Options
--HEAD
	Install HEAD version
==> Analytics

$ls /opt/homebrew/Cellar/gcc/11.2.0/bin
# This should show the list of files one of which will be g++-<version>.


```
* Edit the file `C++ Single File.sublime-build` to have the same binary name as above.
* Go to Sublime Text app (Download from [here](https://www.sublimetext.com) if needed). Go to `Tools` -> `Build System` -> `New Build System...` and copy paste file `C++ Single File.sublime-build` contents into it. Save the file (with a good name to distinguish the build rule)
* Use the new build rule using `Tools` -> `Build System` -> <New file name saved above>
* Add snippet files in this dir (`cpp_stl.sublime-snippet`, `cpptemp.sublime-snippet`, etc.) as new snippets using `Tools` -> `Developer` -> `New Snippets...`. *Note*: Remember to save it with `.sublime-snippet` suffix in filename.
* Now save everything, restart Sublime and use `stltemp` for template, Cmd + B for building.

## Place build file in path in case of manually modifying builds: 

```
/Users/<username>/Library/Application Support/Sublime Text 3/Packages/C++/C++ Single File.sublime-build
```
	
# Steps to fix indentation issue for single line for loop

* Install resource viewer from [here](https://packagecontrol.io/packages/PackageResourceViewer)
* Open `Indentaion Rules.tmPreferences` file using `PackageResourceViewer` -> `Open Resource` -> `C++`
* Replace below:
```
	<key>bracketIndentNextLinePattern</key>
	<string>(?x)
	^ \s* \b(if|while|else)\b [^;]* $
	| ^ \s* \b(for)\b .* $
	</string>
```
* With:
```
	<key>bracketIndentNextLinePattern</key>
	<string>(?x)
	^ \s* \b(if|while|else)\b [^;]* $
	| ^ \s* \b(for)\b [^\)]*\) [^{;]* $
	</string>
```
