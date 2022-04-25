# Python and ArcPy snippets   
   
## Python  
    
### - создаем список
```python
    q_list = [1, 2, 3]   
    q_list = [str(q) for q in q_list]   
``` 
    
### - переводим список в строку через запятую   
```python
    q_list_str = u"'{0}'".format("', '".join([q for q in q_list]))
    str_list = f"{', '.join([str(_['num']) for _ in obj_list])}"
```
       
### - список в условии   
```python
    wc_zones = u"ID IN ('{0}')".format(u"','".join([id for id in list]))
```

### - сцепить список в одну строку
```python
    characters = ['p', 'y', 't', 'h', 'o', 'n']
    word = "".join(characters)
    print(word) # python    
```    
   
### - создание словаря из известного набора ключей с фиксированым значением   
```python
# you can you use dictionary comprehensions:
    keys = ['a', 'b', 'c']
    {k: True for k in keys}
>>> {'a': True, 'b': True, 'c': True}
# However, the dict class has the fromkeys classmethod designed specially for this case:
    dict.fromkeys(keys, True)
>>> {'a': True, 'b': True, 'c': True}    
```        

### - строка из списка:   
```python
    fields_name=', '.join(item for item in [u'ID', u'NAME'])
```   
   
### - строка из случайных символов
```python
    import string
    import random
    name = ''.join([random.choice(string.ascii_uppercase) for _ in range(6)])   
```

### - строка из чисел
```python
def concat_as_numbers(lst: list) -> str:
    return ', '.join(map(str, lst))
```

###  - строка из строк
```python
def concat_as_strings(lst: list) -> str:
    return ", ".join(map(lambda x: f"'{x}'", lst))
```
   
### - datetime из строки
```python
    datetime.datetime.strptime('2019-09-17 15:20:35.123', '%Y-%m-%d %H:%M:%S.%f')
```
   
### - строка из datetime
```python
    datetime_str = <datetime object>.strftime('%Y-%m-%d %H:%M:%S.%f') -> '2019-09-17 15:20:35.123'
```
     
### - форматирование строки с лидирующими нулями
```python
    print '{0:05d}'.format(i) -> 000001
```
    
### - форматирование в Python 3
```python
    print(f"{'Username'}:25}{'Role':20}{'License Type'}")
    print(f"{'-' * 23}{' ' * 2}{'-' * 18}{' ' * 2}{'-' * 15}")
    for user in user_list:
        print(f"{user.username:25}{user.role:20}{user.userLicenseTypeId}")
```
       
### - кодировки   
```python
    from os import environ
    environ['NLS_LANG'] = 'RUSSIAN_CIS.CL8MSWIN1251'
    environ['NLS_LANG'] = 'American_America.AL32UTF8'    
```
   
### - сохранение в файл
```python
    def save_to_file(file_name, data):
        with open(file_name, 'a') as f:
            f.write('{0}\n'.format(data))
            # log_file.write('{0}\n'.format(message.encode('cp1251')))     
```   
   
### - работа с именованными (keyword) аргументами   
```python
# **kwargs (https://realpython.com/python-kwargs-and-args/)
    def test(**kwargs):
        print kwargs['a']
        print kwargs['b']
    
test(a='asdf', b='zxcv')
>>asdf
>>zxcv
```
   
### - progress bar
```python
    import time
    from progress.bar import IncrementalBar
        mylist = [1,2,3,4,5,6,7,8]
        bar = IncrementalBar('Countdown', max = len(mylist))
        for item in mylist:
            bar.next()
            time.sleep(1)
        bar.finish()   
```
   
### - еще пример progressbar 
```python
    from tqdm import tqdm

    def do_download():
        pbar = tqdm(desc='{}_{}'.format(track.get_type(), track.id), total=int(file_size), unit="bytes", unit_scale=True, position=bar_position)
        downloaded_size = 0
        with open(output_file, 'wb') as fd:
            try:
                r = self.client.get_track_download(track)
                for chunk in r.iter_content(1024):
                    fd.write(chunk)
                    downloaded_size += len(chunk)
                    pbar.update(len(chunk))
            except requests.RequestException as e:
                self.logger.debug("requests download error for track {}_{}, exiting".format(track.get_type(), track.id))
                exit(1)
            except:
                exit(1)
        pbar.close()   
```   
   
### - копирование папки с сохранением структуры
```python
    def copytree(src, dst, symlinks=False, ignore=None):
        for item in os.listdir(src):
            s = os.path.join(src, item)
            d = os.path.join(dst, item)
            if os.path.isdir(s):
                shutil.copytree(s, d, symlinks, ignore)
            else:
                shutil.copy2(s, d)   
```       

### - проверка XML на соответствие схеме    
```python        
    try:
        xmlschema.assertValid(xml_to_validate)
    except etree.DocumentInvalid, xml_errors:
        pass
    print "List of errors:\r\n", xml_errors.error_log

    try:
       xmlschema_doc = lxml.etree.parse(filename)
       xmlschema = lxml.etree.XMLSchema(xmlschema_doc)
       xmlschema.assertValid(elem_tree)
    except lxml.etree.ParseError as e:
       raise lxml.etree.ParserError(str(e))
    except lxml.etree.DocumentInvalid as e:
       if ignore_errors:
        raise lxml.etree.ValidationError("The Config tree is invalid with error message:\n\n" + str(e)) 
```

### - Работа с итератором
```python
    iterator = iter(iterable)
    try:
        while True:
            item = next(iterator)
            do_stuff(item)
    except StopIteration:
        pass
    finally:
        del iterator 
```
    
### - кастомный класс ошибки
```python    
    class MyCustomError(Exception):
        def __init__(self, *args):
            if args:
                self.message = args[0]
            else:
                self.message = None

        def __str__(self):
            print('calling str')
            if self.message:
                return 'MyCustomError, {0} '.format(self.message)
            else:
                return 'MyCustomError has been raised'

# raise MyCustomError
raise MyCustomError('We have a problem')
```
   
### - пример создания dataclass (Python 3.7 and over)
```python
    from dataclasses import dataclass
    from typing import List

    @dataclass
    class Sale:
        quantity: int

    @dataclass
    class Product:
        id: str
        name: str
        sales: List[Sale]
```
---          
```python
    from dataclasses import dataclass

    @dataclass
    class InventoryItem:
        name: str
        unit_price: float
        quantity: int = 0

        def total_cost(self) -> float:
            return self.unit_price * self.quantity

item = InventoryItem(name="", unit_price=12, quantity=100)
print(item.total_cost())    # 1200
```       
   
### - сохранение / загрузка json данных 
```python
    import json
    with open(<dump_file_name>, 'w', encoding='utf-8') as outfile:    
        json.dump(<data_dict>, outfile, ensure_ascii=False)   
        
    with open(<dump_file_name>) as json_file:
        data = json.load(json_file)
```
   
   
---
---   

## ArcPy & ArcGIS   
    
### - работа с тулбоксом
```python    
    # При обновлении набора инструментов Python происходит обновление только самого файла 
    # набора инструментов — импортированные в его состав модули не затрагиваются. 
    # Для перезагрузки модуля из набора инструментов Python используйте функцию importlib модуля reload, 
    # которая может быть временно добавлена.
    import yourmodule
    import importlib
    importlib.reload(yourmodule)  # force reload of the module 
```
    
### - нотации: математическая, геодезическая    
- X - Долгота (на восток)   
- Y - Широта (на север)   
   
### - создание полей в feature class или table   
```python
    fields = [
        ("LONG", "LONG", "", "", "", "Длинное целое", "NULLABLE", "NON_REQUIRED", ""), 
        ("SHORT", "SHORT", "", "", "", "Короткое целое", "NULLABLE", "NON_REQUIRED", ""),
        ("TEXT", "TEXT", "", "", 64, "Текст", "NULLABLE", "NON_REQUIRED", ""),
        ("DOUBLE", "DOUBLE", 15, 8, "", "С плавающей точкой", "NULLABLE", "NON_REQUIRED", ""),
        ("DATE", "DATE", "", "", "", "Дата", "NULLABLE", "NON_REQUIRED", "")
    ]
    for field in fields:
        arcpy.AddField_management(*(self.memory_table,) + field)    
``` 

### - работа с курсорами (Cursor)   
```python 
    with arcpy.da.SearchCursor(fc, ['fieldA', 'fieldB']) as cursor:
        for row in cursor:
            print(row)
        
    with arcpy.da.UpdateCursor("c:/base/data.gdb/roads", ["roadtype", "distance"]) as cursor:
        for row in cursor:
            row[1] = row[0] * 100
            cursor.updateRow(row)
        
    with arcpy.da.InsertCursor(fc, ['ID', 'USER_NAME', 'CREATE_DATE', 'FORM_TYPE']) as ins_cursor:
        ins_cursor.insertRow((_id, _user_name, _today, _form_type))
        # получение OBJECTID вставленного объекта
        ioid = ins_cursor.insertRow((_id, _user_name, _today, _form_type))
        print(ioid)
```  
   
### - проверить есть ли записи в курсоре
```python
    if any(arcpy.da.SearchCursor(FeatureClass, fieldnames, whereClause)):
        есть
    else:
        нет
```    

### - узнать количество записей в курсоре   
```python
# способ 1:
    with arcpy.da.SearchCursor(FeatureClass, fieldnames, where_clause) as srcToday:
        count = sum(1 for row in srcToday)
# способ 2:
    featureList = [row[0] for row in arcpy.da.SearchCursor(FeatureClass, fieldnames, where_clause) ]
    count = len(featureList)
```
    
### - работа с Редактором (Editor)
```python
edit = arcpy.da.Editor(sdeconnection)
try:
    edit.startEditing(False, False)
    edit.startOperation()
    # непосредственно операции
    with arcpy.da.InsertCursor(fc, fields) as fc_icursor:
        fc_icursor.insertRow(someNewRow)
    edit.stopOperation()
    edit.stopEditing(True)  ## Stop the edit session with True to save the changes
except Exception as err:
    if edit.isEditing:
        edit.stopOperation()
        edit.stopEditing(False)  ## Stop the edit session with False to abandon the changes
finally:
    # Cleanup
    arcpy.ClearWorkspaceCache_management()‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍‍
```
    
### - получение JSON в ArcMap
```python 
import arcpy
lyr = 'lyr'
arcpy.MakeFeatureLayer_management(<Название класса>, lyr)
arcpy.FeatureSet(lyr).JSON
```
   
### - список полей в таблице raw_table
```python
exclude_flds = ['OBJECTID']
raw_table_flds = [fld.name for fld in arcpy.ListFields(raw_table) if fld.name not in exclude_flds]
print (raw_table_flds)
```

### - расчет в поле автоинкримента (ArcMap)   
```python
rec=0 
def autoIncrement(): 
    global rec 
    pStart = 1  
    pInterval = 1 
    if (rec == 0):  
        rec = pStart  
    else:  
        rec += pInterval  
    return rec
```
       
### - расчет в поле GUID (ArcMap)    
```python
def calc():
    from uuid import uuid4
    return u'{{{0}}}'.format(uuid4()).upper()
```
### - случайное значение из диапазона (ArcMap)
```python
def get_val(val):
    import random
    random_val = random.randint(-10,10)
    if val != 0:
        return val + random_val
    else:
        return val
        
def get_val(val):
    import random
    random_val = random.randint(-50000,50000)
    if val != 0:
        ret_val = val + random_val
        if ret_val < 0:
            return abs(ret_val)
        else:
            return ret_val
    else:
        return val
```
   
### - сдвиг точки на угол и расстояние FieldCalculator (shiftXYCoordinates(!SHAPE!, !Angle! ,5000))
```python
def shiftXYCoordinates(shape,angle,distance):
    point = shape.getPart(0)
    point.Y += distance * math.cos(math.radians(angle))
    point.X += distance * math.sin(math.radians(angle))
    return point     
```
   
   
---   

# PANDAS

### - класс ArcGIS в датафрейм
```python
import pandas
fc = # path to feature class
df = pandas.DataFrame(
    arcpy.da.FeatureClassToNumPyArray(
        fc,
        [fld.name for fld in arcpy.ListFields(fc) if fld.name != arcpy.Describe(fc).shapeFieldName]
    )
)
```    
    
