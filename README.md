# Python 3 "Black Hat Python" Source Code

Source code for the book *Black Hat Python* by Justin Seitz. The code has been fully converted to Python 3, reformatted to comply with PEP8 standards, and refactored to eliminate dependency issues involving deprecated libraries.

Although many optimizations could have been implemented in the source code presented throughout the book, the code was left unaltered as much as possible to allow readers to apply such modifications as they see fit. The code, as it is, requires serious refactoring efforts ranging from docstrings to type hinting and exception handling, not to mention enhancements like context managers. However, these issues may benefit readers by encouraging them to implement these improvements. Many bugs, primarily related to indentation, have been corrected to prevent fatal errors during runtime.

*A similar conversion has been made available by me for the source code of the book *Violent Python* by TJ O'Connor. Check it out [here](https://github.com/EONRaider/violent-python3) if you haven't done so yet.*

## Usage

Simply choose a directory (DIR) to clone the project using `git clone`, create a new virtual environment (`venv`) for it (recommended), and install the requirements using `pip install`:

```bash
user@host:~/DIR$ git clone https://github.com/EONRaider/blackhat-python3
user@host:~/DIR$ python3 -m venv venv
user@host:~/DIR$ source venv/bin/activate
(venv) user@host:~/DIR$ pip install -r requirements.txt
```

## Notes

- Some listings presented in the book were missing from the author's code repository (available on the *No Starch Press* website) and have been added to their respective chapters. A more accurate naming convention has been applied to the files to relate them to the book's code.
- Minor bugs that generated warnings from the interpreter have been fixed without altering the code's core characteristics.
- Auxiliary files required to make the code work have been added to their respective chapters.
- On a personal note, the author could have written cleaner code without jeopardizing the quickness required for ethical hacking engagements. Why this wasn't done remains unclear.

## Refactoring

Critical bug fixes made to ensure proper implementation and to avoid fatal errors:

- **`chapter02/bh_sshserver.py`**: Required the RSA key from the `test_rsa.key` file, now included in the corresponding directory.
- **`chapter03/sniffer_ip_header_decode.py`**, **`sniffer_with_icmp.py`**, and **`scanner.py`**: Had significant issues in IP packet size definitions and 32/64-bit portability due to problems in `struct`. More details can be found in [this Stack Overflow thread](https://stackoverflow.com/questions/29306747/python-sniffing-from-black-hat-python-book#29307402).
- **`chapter03/scanner.py`**: Used the `netaddr` library, which is no longer maintained and incompatible with Python 3. It has been refactored to use the `ipaddress` module from Python's standard library.
- **`chapter04/arper.py`** and **`mail_sniffer.py`**: Used the `scapy` library, which is incompatible with Python 3. The code now uses the `kamene` library.
- **`chapter04/pic_carver.py`**: Replaced the deprecated `cv2.cv` module with the `opencv-python` library. Parameters were updated according to [this commit](https://github.com/ragulin/face-recognition-server/commit/7b9773be352cbcd8a3aff50c7371f8aaf737bc5c).
- **`chapter05/content_bruter.py`** and **`joomla_killer.py`**: Added required wordlists (`all.txt` and `cain.txt`) to their respective chapters.
- **`chapter06/bhp_bing.py`**, **`bhp_fuzzer.py`**, and **`bhp_wordlist.py`**: Reformatted to comply with PEP8 standards, though some warnings persist due to specific class naming conventions required by Burp Suite.
- **`chapter07/git_trojan.py`**: Refactored to replace the deprecated `imp` library with `types`. A subdirectory structure and configuration files were added, and a missing relative path in the "trojan_config" variable was corrected. A call to the `to_tree` method was added to avoid `AttributeError`.
- **`chapter08/keylogger.py`**: Requires the `PyHook` library. A wheel file for version 1.6.2 has been included. Other versions can be downloaded [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pyhook).
- **`chapter09/ie_exfil.py`**: Fixed errors in handling the `plaintext` variable (string vs binary string) in the `encrypt_string` function. Corrected the use of the `base64` library. Thanks to [Enraged](https://github.com/Enraged) for their contribution in [this commit](https://github.com/EONRaider/blackhat-python3/pull/2/commits/fcab6afc19fc4ea01b8c5c475e7b8c5e4b158df6).

## Translations

Contributions in other languages:

- [Turkish](https://github.com/EONRaider/blackhat-python3/tree/turkish-language) by [Bedirhan Budak](https://github.com/bedirhanbudak)

## Contributing

To contribute, discuss your proposed changes via an issue before making modifications.

1. Ensure your modifications justify a pull request. Minor changes (1–2 lines) should be requested through an issue.
2. Update the `README.md` file if necessary to reflect project structure changes.
3. Follow a commit message standard. Refer to [this guide](https://chris.beams.io/posts/git-commit/) if unsure.
4. Your request will be reviewed within 48 hours.

---