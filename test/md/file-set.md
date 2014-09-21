<a name="module_file-set"></a>
##file-set
Exports a contructor taking a list of file patterns as input, returning a `file-set` instance containing the expanded patterns split into separate lists of `files`, `dirs` and `notExisting`.

**Example**  
```js
var fileSet = require("file-set");
```

<a name="exp_module_file-set^FileSet"></a>
###class: FileSet ⏏
Expands file patterns, returning the matched and unmatched files and directories

<a name="new_module_file-set^FileSet◊"></a>
####new FileSet(patternList)
**Params**

- patternList `string` | `Array.<string>` - A pattern, or array of patterns to expand  

<a name="module_file-set^FileSet#list"></a>
####fileSet.list
The full list of unique paths found, and not found.

<a name="module_file-set^FileSet#files"></a>
####fileSet.files
The existing files found

<a name="module_file-set^FileSet#dirs"></a>
####fileSet.dirs
The existing directories found

<a name="module_file-set^FileSet#notExisting"></a>
####fileSet.notExisting
Paths which were not found

<a name="module_file-set^FileSet#add"></a>
####fileSet.add(files)
add file patterns to the set

**Params**

- files `string` | `Array.<string>` - A pattern, or array of patterns to expand  

<a name="module_file-set^FileSet.eFileType"></a>
####FileSet.eFileType
Enum for the `type` value of each record in `fileSet.list`
