# GitLab Adaptation of md_file_tree.py

**Note: This is a modification of https://github.com/amaiorano/md-to-toc

## Cosmetic Changes

### Directory Label
- Original output: **Directory Label/**
```
- **Directory Label/**
```
- Modified output: **Directory Label**
```
- **Directory Label**
```

### Nested file name and link
- Original output: Name.md
```
- [Name.md](.\\Directory1\\Directory2\\Name.md)
```
- Mofified output: Name
```
- [Name](.Directory1/Directory2/Name)
```

## Code Changes
### Edits to Directory Label
- Original code at line 106
```python
if len(files) > 0:
            level = root.count(os.sep) - base_level
            indent = '  ' * level
            if root != cwd:
                indent = '  ' * (level - 1)
                md_lines.append('{0} {2} **{1}/**\n'.format(indent,
                                                            os.path.basename(root),
                                                            TOC_LIST_PREFIX))
```
- Modified code (removed 1 symbol)
```
if len(files) > 0:
            level = root.count(os.sep) - base_level
            indent = '  ' * level
            if root != cwd:
                indent = '  ' * (level - 1)
                md_lines.append('{0} {2} **{1}**\n'.format(indent,                  # Removed '/' after the {1}
                                                            os.path.basename(root),
                                                            TOC_LIST_PREFIX))
```
### Edits to nested file name and link
- Original code at line 114
```python
rel_dir = '.{1}{0}'.format(os.sep, root[base_len:])
            for md_filename in files:
                indent = '  ' * level
                if wikilinks:
                    md_lines.append('{0} {3} [[{2}{1}]]\n'.format(indent,
                                                                  os.path.splitext(md_filename)[0],
                                                                  rel_dir,
                                                                  TOC_LIST_PREFIX))
                else:
                    md_lines.append('{0} {3} [{1}]({2}{1})\n'.format(indent,
                                                                     md_filename,
                                                                     rel_dir,
                                                                     TOC_LIST_PREFIX))
```
- Modified code (added 3 lines)
```python
rel_dir = '.{1}{0}'.format(os.sep, root[base_len:])
            for md_filename in files:
                indent = '  ' * level
                rel_dir = rel_dir.replace('.\\','.')            # Remove '.\\' from the front of the file link
                rel_dir = rel_dir.replace('\\','/')             # Replace '\\' from the file link path with '/'
                md_filename = md_filename.replace('.md','')     # Remove the '.md' from the file name and link
                if wikilinks:
                    md_lines.append('{0} {3} [[{2}{1}]]\n'.format(indent,
                                                                  os.path.splitext(md_filename)[0],
                                                                  rel_dir,
                                                                  TOC_LIST_PREFIX))
                else:
                    md_lines.append('{0} {3} [{1}]({2}{1})\n'.format(indent,
                                                                     md_filename,
                                                                     rel_dir,
                                                                     TOC_LIST_PREFIX))
```
