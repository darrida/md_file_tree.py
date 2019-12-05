# GitLab Adaptation of md_file_tree.py

**Note: This is a modification of https://github.com/amaiorano/md-to-toc

## Changes

### Directory Label
- Original output:
```python
- **Directory Label/**
```
- Modified output:
```
- **Directory Label**
```

### Nested file link
- Original output:
```python
[Name.md](.\\Directory1\\Directory2\\Name.md)
```
- Mofified output:
```
[Name](.Directory1/Directory2/Name)
```
