# Config

### ranger

修改ranger的默认的文本编译器为nvim

```bash
~/.config/ranger/rifle.conf

#------------------
# Misc
# ------------------
# Define the "editor"
mine ^text, label editor = nvim -- "$@"
!mine ^text, label editor, ext xml|json|csv|texpy|pl|rb|js|sh|php = nvim -- "$@"
```

