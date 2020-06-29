  This is the best known method to implement yocto linux versioning.

  1.Edit  meta/recipes-core/os-release/os-release.bb to something like this below:
  ID = "${DISTRO}"
  NAME = "${DISTRO_NAME}"
  VERSION = "${DISTRO_VERSION}${@' (%s)' % DISTRO_CODENAME if 'DISTRO_CODENAME' in d else ''}"
  VERSION_ID = "${DISTRO_VERSION}"
  PRETTY_NAME = "${DISTRO_NAME} ${VERSION}"
  BUILD_ID ?= "${DATETIME}"
  BUILD_ID[vardepsexclude] = "DATETIME"

  OS_RELEASE_FIELDS += "BUILD_VERSION"
  BUG_FIXED_VERSION = "1.0.0-B1"
  BUILD_VERSION = "${BUG_FIXED_VERSION}"

  2. Go back to build directory, bitbake os-release

  3.If bitbake os-release run succcessfully, bitbake the image again 

  4. Unzip the tar file in a local folder

  5. navigate to /etc and observe os-release is available.

  kj@kj-Aspire-V3-471G:~/untap_fs/etc$ cat os-release
  ID="poky"
  NAME="Poky (Yocto Project Reference Distro)"
  VERSION="3.0+snapshot-20200629 (master)"
  VERSION_ID="3.0-snapshot-20200629"
  PRETTY_NAME="Poky (Yocto Project Reference Distro) 3.0+snapshot-20200629 (master)"
  BUILD_VERSION="1.0.0-B1"
