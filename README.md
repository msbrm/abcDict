# abcDict

## example

```yaml
# abctest.yaml
path: ${ALLUSERSPROFILE}

info:
  none1: ''
  none2: None
  name: ${name}
  name_default: ${name|default:msbrm}
  age: ${age}
  age_default: ${age|default:18}
  age_default_int: ${age|default:18|type:int}

info_str: 我是name:${name},name_default:${name|default:$<name>},今年刚满age:${age},age_default:${age|default:18}岁
info_str2: ${HOME}xxxxxxx${age|default:18|type:int}xxxxxxx${HOME}
file_path: /home/${FILE|default:abc}/abc.test
```

```python
# abctest.py
import sys
from pathlib import Path

FILE_PATH = Path(__file__)

sys.path.append(str(FILE_PATH.parent.parent))

from src import AbcDict

yaml_file = FILE_PATH.with_suffix('.yaml')

abcDict = AbcDict(yaml_file)

print(abcDict.path)
print(abcDict.info.age_default_int)
print(type(abcDict.info.age_default_int))
print(abcDict)

abcDict.dump(yaml_file.with_stem('save'))  # save as save.yaml
```

```txt
# cmd output
> python .\test\abctest.py
C:\ProgramData
18
<class 'int'>
{'path': 'C:\\ProgramData', 'info': {'none1': '', 'none2': 'None', 'name': None, 'name_default': 'msbrm', 'age': None, 'age_default': '18', 'age_default_int': 18}, 'info_str': '我是name:None,name_default:$<name>,今年刚满age:None,age_default:18岁', 'info_str2': 'C:\\Users\\Administratorxxxxxxx18xxxxxxxC:\\Users\\Administrator', 'file_path': '/home/abc/abc.test'}
```

```yaml
# save.yaml
file_path: /home/abc/abc.test
info:
  age: null
  age_default: '18'
  age_default_int: 18
  name: null
  name_default: msbrm
  none1: ''
  none2: None
info_str: 我是name:None,name_default:$<name>,今年刚满age:None,age_default:18岁
info_str2: C:\Users\Administratorxxxxxxx18xxxxxxxC:\Users\Administrator
path: C:\ProgramData
```
