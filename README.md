# ompl Code Format
Why waste your valuable development time formatting code manually when we are trying to build amazing robots?

The repo contains an auto formatting script for the [OMPL C++ Style Guidelines](http://ompl.kavrakilab.org/styleGuide.html).

> **Note: this style is in beta format, please submit suggestions or fixes!**

## Setup

 * Install **clang_format**:

   ``sudo apt-get install -y clang-format-3.6``

 * Then symlink or copy in the root of your ompl directory the file ``.clang_format``, located in this repo. You can save this file from [this link](https://raw.githubusercontent.com/davetcoleman/ompl_code_format/master/.clang-format). For example, place it on your computer here:

   ``~/ompl/.clang_format``

 * If you are interested in improving this configuration file, we recommend you checkout the git repo and symlink, e.g.:

   ``ln -s ~/ompl_code_format/.clang-format ~/ompl/.clang-format``

 * Now any file inside your catkin workspace will be formatted with the OMPL style guidelines described in this config file

## Usage

You can run **clang_format** in several ways:

### Command Line

Format single file:

    clang-format-3.6 --i -style=file MY_OMPL_FILE.cpp

Format entire directory recursively including subfolders:

    find . -name '*.h' -or -name '*.hpp' -or -name '*.cpp' | xargs clang-format-3.6 --i -style=file $1

### Emacs Editor Configuration

In your ``~/.emacs`` config file, add the following:

Format your source code if its in some directory such as the ``ompl`` (feel free to change keywords ompl):

```
(defun run-ompl-clang-format ()
  "Runs clang-format on cpp,h files in ompl/ and reverts buffer."
  (interactive)
  (and
   (string-match "/ompl/.*\\.\\(h\\|cpp\\)$" buffer-file-name)
   (save-some-buffers 'no-confirm)
   (shell-command (concat "clang-format-3.6 -style=file -i " buffer-file-name))
   (message (concat "Saved and ran clang-format on " buffer-file-name))
   (revert-buffer t t t)
))
```

Set a keyboard shortcut to run, such as F12

    (global-set-key [f12] 'run-ompl-clang-format)

### Atom Editor Configuration

Install the [clang-format](https://atom.io/packages/clang-format) package via the Atom package manager or ``apm install clang-format``.

In the package settings set ``clang-format-3.6`` as your executable and point 'Style' to your ``.clang_format`` file.
