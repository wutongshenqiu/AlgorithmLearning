## 一次读一行

- 使用 `cin` 进行字符串的读取时，遇到空格或者换行符就会停止，如果我们需要一次读取一行字符串，可以使用 [`getline()`](http://www.cplusplus.com/reference/string/string/getline/)
- `cin` 不会读取换行符或者空格，因此在使用 `getline()` 前如果有使用过 `cin`，那么最好先使用 `getchar()`