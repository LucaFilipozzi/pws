# pws

A reimplementation of Peter Palfrader's [pwstore][1]
- implemented in ruby, leveraging [ruby-gpgme][3] and [thor][4]
- command line interface differs: 'new' for 'ed -n', 'mod' for 'ed', 'enc' for 'rc'
- compatible with `~/.pws.yaml` but not `~/.pws-trusted-users`
~ compatible with `dir/.users`
- ignores `dir/.keyring` however

Ultimately, the purpose of both [pwstore][1] and this reimplementation is
two-fold:
- to ensure that the encryption recipients are correct and complete by
  validating access lines (first line of a file) against the users and groups
  defined in `~/.users`
- to prevent plaintext copies from being generated by leveraging ruby's
  [Tempfile][2] class which automatically deletes the temporary file when the
  object goes out of scope, and invoking the editor through a subshell

Two challenges remain:
- determine whether [ruby-gpgme][3] permits the use of an alternate keyring: this would
  allow this reimplementation to make use of `dir/.keyring`
- determine whether [ruby-gpgme][3] could emit the encryption recipients of an encrypted
  file without explicitly decrypting it (by examining the underlying packets): this would
  allow the 'dir' command to be implemented so that encrypted files may be verified as
  having been encrypted for the appropriate recipients

[1]: https://github.com/weaselp/pwstore
[2]: http://ruby-doc.org/stdlib-2.2.3/libdoc/tempfile/rdoc/Tempfile.html
[3]: https://github.com/ueno/ruby-gpgme
[4]: https://github.com/erikhuda/thor
