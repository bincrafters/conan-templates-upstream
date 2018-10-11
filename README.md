# Template for upstream in-source Conan recipes

## Usage
  1. Copy the `conan/` directory into the upstream project
  2. Create a `conanfile.py` with the recipe, you can use [this template file](https://github.com/bincrafters/conan-templates/blob/master/conanfile.py)
    * change the `source` method to:
      ```     
      def source(self):
          # Wrap the original CMake file to call conan_basic_setup
          shutil.move("CMakeLists.txt", "CMakeListsOriginal.txt")
          shutil.move(os.path.join("conan", "CMakeLists.txt"), "CMakeLists.txt")
      ```
  3. Open the `.travis.yml`, search for `TODO` and follow the explanations
  4. Open the `appyevor.yml`, search for `TODO` and follow the explanations
  5. Save the adjusted `.travis.yml` and `appveyor.yml` files in the upstream project
  6. Set the following environment variables in the Travis and AppVeyor UI (**don't forget encryption**):
    * `CONAN_UPLOAD`: API URL to your Conan repository (most likely Bintray)
    * `CONAN_LOGIN_USERNAME`: Your Conan repository username (e.g. Bintray username)
    * `CONAN_PASSWORD` Your Conan repository password (e.g. Bintray API key)

## Features
  * generic files across different projects for easy maintainance and future updates
  * easily configurable through environment variables
  * builds and uploads packages on git tag pushes
    * it uses the name of the git tag as version
    * it removes the `v` from the git tag (if there is one)
  * uploads the recipe-only as a master version on pushes to the master branch
    * this can be easily removed
  * tests on every non-tag and non-master push a single `conan create` build on every OS


## Issue tracker
The issue tracker can be found here: https://github.com/bincrafters/community/issues

## Stability
### DO NOT INTRODUCE BREAKING BEHAVIOUR
Only if it is absolutely neccessary or the benefits are extremely huge. If there are breaking changes **document them in this readme**. These templates are meant to be shared between very different projects with different setups and building environments and it's a terrible idea to start maintaining these files seperately for all of these projects.


## Known projects which are using a version of this template
  * [google/flatbuffers](https://github.com/google/flatbuffers)
