[update-readmes]   Mode: rewrite — migrating to template structure...
# fs_shim.dart

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/fs_shim.dart)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/fs_shim.dart.git
cd fs_shim.dart
```

## Usage



### Using IO API

#### Setup

Replace

    import 'dart:io';

with

    import 'package:fs_shim/fs_io.dart';

Then a reduced set of the IO API can be used, same source code that might requires some cleanup if you import from
existing code

#### Simple example

````
import 'package:fs_shim/fs_io.dart';
import 'package:path/path.dart';

main() async {
  FileSystem fs = ioFileSystem;
  // safe place when running from package root
  String dirPath = join(Directory.current.path, 'test_out', 'example', 'dir');

  // Create a top level directory
  // fs.directory('/dir');
  Directory dir = new Directory(dirPath);

  // delete its content
  await dir.delete(recursive: true);

  // and a file in it
  // fs.file(join(dir.path, "file"));
  File file = new File(join(dir.path, "file"));

  // create a file
  await file.create(recursive: true);
  await file.writeAsString("Hello world!");

  // read a file
  print('file: ${await file.readAsString()}');

  // use a file link if supported
  if (fs.supportsFileLink) {
    // fs.link(join(dir.path, "link"));
    Link link = new Link(join(dir.path, "link"));
    await link.create(file.path);

    print('link: ${await new File(link.path).readAsString()}');
  }

  // list dir content
  print(await dir.list(recursive: true, followLinks: true).toList());
}
````

### In memory

A simple usage example:

````
import 'package:fs_shim/fs.dart';
import 'package:fs_shim/fs_memory.dart';
import 'package:path/path.dart';

main() async {
  FileSystem fs = newMemoryFileSystem();

  // Create a top level directory
  Directory dir = fs.directory('/dir');

  // and a file in it
  File file = fs.file(join(dir.path, "file"));

  // create a file
  await file.create(recursive: true);
  await file.writeAsString("Hello world!");

  // read a file
  print('file: ${await file.readAsString()}');

  // use a file link if supported
  if (fs.supportsFileLink) {
    Link link = fs.link(join(dir.path, "link"));
    await link.create(file.path);

    print('link: ${await fs.file(link.path).readAsString()}');
  }

  // list dir content
  print(await dir.list(recursive: true, followLinks: true).toList());
}
````

### Browser usage

```dart
import 'package:fs_shim/fs_browser.dart';
import 'package:fs_shim/fs_idb.dart';

FileSystem fs = fileSystemIdb;
```


### Node

#### Setup

pubspec.yaml:

```yaml
dependency:
  tekartik_fs_node:
    git:
      url: https://github.com/tekartik/fs_shim.dart
      path: fs_node
```

A simple usage example:

````dart
import 'package:tekartik_fs_node/fs.dart';
import 'package:path/path.dart';

main() async {
  FileSystem fs = fileSystemNode;
  ...
````  

### Utilities

* Lightweight glob support (`**`, `*` and `?` in a posix style path)
* Copy utilities (copy files, directories recursively)

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/fs_shim.dart`](https://github.com/Interested-Deving-1896/fs_shim.dart) and mirrored through:

```
Interested-Deving-1896/fs_shim.dart  ──►  OpenOS-Project-OSP/fs_shim.dart  ──►  OpenOS-Project-Ecosystem-OOC/fs_shim.dart
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[BSD-2-Clause](https://github.com/Interested-Deving-1896/fs_shim.dart/blob/master/LICENSE) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
