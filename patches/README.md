# CCP Python Module Modifications

These patch files keep track of changes made to files sourced from upstream cpython repo https://github.com/python/cpython. Please make sure to generate new patch files when you make changes to their corresponding source files.

When updating to a new Python version fresh copies of those files should be placed in the repo. Then the patches should be applied either manually by hand, or using whatever tools you like. Be mindful that not all changes required are necessarily going to be included in the patch. For example the socket module has been converted from C to C++, so any C++ incompatible changes will have to be fixed up.

Upstream bases differ by file. Apply each patch against the release listed for that file — do not assume a single repo-wide base.

Mapping of files sourced from Python:

| cpython                         | carbon-io                                      | upstream base |
|---------------------------------|------------------------------------------------|---------------|
| Modules/socketmodule.h          | include/socketmodule.h                         | v3.12.16      |
| Modules/_ssl/clinic/cert.c.h    | src/_ssl/clinic/cert.c.h                       | v3.13.15      |
| Modules/_ssl/cert.c             | src/_ssl/cert.c                                | v3.12.3       |
| Modules/_ssl/debughelpers.c     | src/_ssl/debughelpers.c                        | v3.13.15      |
| Modules/_ssl/misc.c             | src/_ssl/misc.c                                | v3.12.3       |
| Modules/clinic/_ssl.c.h         | src/clinic/_ssl.c.h                            | v3.13.15      |
| Modules/clinic/selectmodule.c.h | src/clinic/selectmodule.c.h                    | v3.13.15      |
| Modules/clinic/socketmodule.c.h | src/clinic/socketmodule.c.h                    | v3.12.16\*    |
| Modules/_ssl.c                  | src/_ssl.c                                     | v3.13.15      |
| Modules/_ssl.h                  | src/_ssl.h                                     | v3.12.3       |
| Modules/_ssl_data_31.h          | src/_ssl_data_31.h                             | v3.12.3       |
| Modules/_ssl_data_111.h         | src/_ssl_data_111.h                            | v3.12.3       |
| Modules/_ssl_data_300.h         | src/_ssl_data_300.h                            | v3.12.3       |
| Modules/addrinfo.h              | src/addrinfo.h                                 | v3.12.3       |
| Modules/selectmodule.c          | src/selectmodule.c                             | v3.13.15      |
| Modules/socketmodule.c          | src/socketmodule.cpp                           | v3.12.16      |
| Lib/test/certdata               | tests/python/carboniotests/test/certdata       | v3.12.16      |
| Lib/test/test_select.py         | tests/python/carboniotests/test/test_select.py | v3.12.16      |
| Lib/test/test_socket.py         | tests/python/carboniotests/test/test_socket.py | v3.12.16      |
| Lib/test/test_ssl.py            | tests/python/carboniotests/test/test_ssl.py    | v3.12.16      |
| Lib/test/ssl_servers.py         | tests/python/ssl_servers.py                    | v3.12.16      |

\* `socketmodule.c.h` was regenerated with CPython 3.13.15 Argument Clinic, then adapted for MSVC C++ (`_PyArg_Parser` sequential assignment); its record is against the v3.12.16 stock file, like `socketmodule.cpp`, which follows upstream carbon-io 1.5.0 onto 3.12.16 and was never re-vendored onto 3.13.

mobile-exp merges upstream carbon-io 1.5.0 but keeps the CPython 3.13.15 `_ssl` sources (`src/_ssl.c`, `src/_ssl/`) and select sources as they were. In particular `Modules/_ssl/distrusted_spki.h` (the eMudhra distrust check, gh-160040, which upstream took from 3.12.16) is not vendored: on the 3.13 line it arrives with 3.13.18, and it comes with the python3 upgrade. `test_ssl.py`'s `test_distrusted_spki` is skipped until then.

`Modules/_ssl_data.h` is no longer vendored: CPython 3.13 replaced its fallback branch with `#error`.

Release tags:
- v3.12.3 — `f6650f9ad73359051f3e558c2431a109bc016664`
- v3.12.16 — `2c2462afc5d978d31f3d073001fc202d269917ff`
- v3.13.15 — `4061bc4c35f7c26f25264666d4ba083b93d2f6f9`
