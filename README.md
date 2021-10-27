# Steps to install GNU GCC on Mac

* If multiuser mac ([reference](https://docs.brew.sh/Installation#untar-anywhere)):
  * Run this command to install separate homebrew in home dir: `mkdir homebrew && curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew`
  * Set homebrew from new installation in `PATH` var: `export PATH=$HOME/homebrew/bin:$PATH >> ~/.zshrc # or ~/.bashrc`
  * Verify new installation using `which brew`
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
	
# Steps to set `subl` in PATH
* Open Applications dir, right click on Sublime text and choose: `Copy "Sublime Text" as Pathname`. Example path: `/Applications/Sublime Text.app`
* In Terminal, do the following: `ls -R /Applications/Sublime\ Text.app` (remember to escape the whitespace.
* There should be one dir with `bin`:
```
/Applications/Sublime Text.app/Contents/SharedSupport/bin:
subl
```
* Add this line to ~/.zprofile: `export PATH=$PATH:/Applications/Sublime\ Text.app/Contents/SharedSupport/bin`
