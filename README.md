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

### Nested file link
- Original output: Name.md
```
- [Name.md](.\\Directory1\\Directory2\\Name.md)
```
- Mofified output: Name
```
- [Name](.Directory1/Directory2/Name)
```

## Code Changes
```
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

```
rel_dir = '.{1}{0}'.format(os.sep, root[base_len:])
            for md_filename in files:
                indent = '  ' * level
                rel_dir = rel_dir.replace('.\\','.')
                rel_dir = rel_dir.replace('\\','/')
                md_filename.replace('.md','')
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
