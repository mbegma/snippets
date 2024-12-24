# Python and ArcPy snippets   
   
## Python   
   
### использование pip
[статья](https://habr.com/ru/articles/806691/)
```python
   pip download <название библиотеки> - скачивается библиотека и все зависимости

   pip install --no-index   --find-links <путь куда ты все положил> <твоя либа>

   pip download -r requirements.txt тоже работает
```
    
### создаем список
```python
    q_list = [1, 2, 3]   
    q_list = [str(q) for q in q_list]   
``` 
    
### оставляет в списке, только уникальные значения   
```python
def do_uniq_values_in_list(lst):
    return list(set(lst))
```
    
### сравнение объектов используя intersection()
```python
list_a = ['Вася', 'Петя', 'Саша']
list_b = ['Лена', 'Катя', 'Саша']
set_a = set(list_a)
set_b = set(list_b)
set_a.intersection(set_b)
>>> {'Саша'}
```    
     
### получение отличных объектов     
```python
set_a = {'Вася', 'Петя', 'Саша'}
set_b = {'Лена', 'Катя', 'Саша'}
set_a.difference(set_b)
>>> {'Вася', 'Петя'}
    
set_a = {'Вася', 'Петя', 'Саша'}
set_b = {'Лена', 'Катя', 'Саша'}
set_b.difference(set_a)
>>> {'Лена', 'Катя'}
```

### уникальные значения в 2х объектах
```python
set_a = {'Вася', 'Петя', 'Саша'}
set_b = {'Лена', 'Катя', 'Саша'}
set_a.symmetric_difference(set_b)
>>> {'Вася', 'Лена', 'Петя', 'Катя'}
```
    
### объединение
```python
set_a = {'Вася', 'Петя', 'Саша'}
set_b = {'Лена', 'Катя', 'Саша'}
set_a.union(set_b)
>>> {'Вася', 'Лена', 'Петя', 'Катя', 'Саша'}
```
    
    
### переводим список в строку через запятую   
```python
    q_list_str = u"'{0}'".format("', '".join([q for q in q_list]))
    str_list = f"{', '.join([str(_['num']) for _ in obj_list])}"     
    lst = ["One", "Two", "Three"]
    str = f"{', '.join([_ for _ in lst])}"
```
       
### список в условии   
```python
    wc_zones = u"ID IN ('{0}')".format(u"','".join([id for id in list]))
```

### сцепить список в одну строку
```python
    characters = ['p', 'y', 't', 'h', 'o', 'n']
    word = "".join(characters)
    print(word) # python    
```    
   
### создание словаря из известного набора ключей с фиксированым значением   
```python
# you can you use dictionary comprehensions:
    keys = ['a', 'b', 'c']
    {k: True for k in keys}
>>> {'a': True, 'b': True, 'c': True}
# However, the dict class has the fromkeys classmethod designed specially for this case:
    dict.fromkeys(keys, True)
>>> {'a': True, 'b': True, 'c': True}    
```        

### строка из списка:   
```python
    fields_name=', '.join(item for item in [u'ID', u'NAME'])
```   
   
### строка из случайных символов
```python
    import string
    import random
    name = ''.join([random.choice(string.ascii_uppercase) for _ in range(6)])   
```

### строка из чисел
```python
def concat_as_numbers(lst: list) -> str:
    return ', '.join(map(str, lst))
```

### строка из строк
```python
def concat_as_strings(lst: list) -> str:
    return ", ".join(map(lambda x: f"'{x}'", lst))
```
   
### datetime из строки
```python
    datetime.datetime.strptime('2019-09-17 15:20:35.123', '%Y-%m-%d %H:%M:%S.%f')
```
   
### строка из datetime
```python
    datetime_str = <datetime object>.strftime('%Y-%m-%d %H:%M:%S.%f')   
    >>> '2019-09-17 15:20:35.123'
        
    datetime_str = f'{<datetime object>:%Y-%m-%d %H:%M:%S}'     
    >>> '2019-09-17 15:20:35.123'   
         
    # ISO 8601 формат, YYYY-MM-DDTHH:MM:SS
    <datetime object>.isoformat() 
    >>> '2019-09-17T15:20:35.123'
```
     
### конвертирование integer timestamp в datetime     
```python 
# datetime.datetime.fromtimestamp() is correct, 
# except you are probably having timestamp in miliseconds (like in JavaScript), 
# but fromtimestamp() expects Unix timestamp, in seconds.
    import datetime   
    your_timestamp = 1669007002000   
    date = datetime.datetime.fromtimestamp(your_timestamp / 1e3)   
      
>> datetime.datetime(2022, 11, 21, 8, 3, 22)
```
   
### прибавить к конкретной дате определенное количество дней в datetime     
```python    
    import datetime
    d1 = datetime.datetime.strptime('1900-01-01 00:00:00.1', '%Y-%m-%d %H:%M:%S.%f')
    d2 = d1 + datetime.timedelta(days=int(d))
    return d2 
```
       
   
### работа с датами в формате ISO-8601 YYYY-MM-DDTHH:mm:ss     
```python
   import dateutil.parser
   
   datetime.datetime.strptime('2022-04-02 04:00:00.001', '%Y-%m-%d %H:%M:%S.%f').isoformat()
   >> {str}'2022-04-02T04:00:00.001000'
   
   dateutil.parser.isoparse(datetime.datetime.strptime('2022-04-02 04:00:00.001', '%Y-%m-%d %H:%M:%S.%f').isoformat())
   >> {datetime} 2022-04-02 04:00:00.001000
   
   dateutil.parser.isoparse('2022-04-02T04:00:00.001000Z')
   >> {datetime} 2022-04-02 04:00:00.001000+00:00
   
```
      
      
### Замена utcnow()
```python
from datetime import datetime, timezone
datetime.now(timezone.utc)
```  
     
      
### Функция возвращает указанное число табуляций     
```python  
def tab(n):
    return "\t" * n
    
>> print (f"{tab(2)} test text")
```    
        
### форматирование строки с лидирующими нулями (только для int)
```python
    number = 1
    print '{0:05d}'.format(number) -> 000001
    # for Python 3.6+  with f-strings:
    print(f"{number:05d}") -> 00001
```
    
### форматирование floats в f-string
```python   
    print(f"Пересечение: {a:.4f}, наклон: {b:.4f}")
    print(f"y = {b:.4f}x + {a:.4f}")
```

### форматирование datetime в f-string
```python   
    import datetime
    now = datetime.datetime.now()
    print(f'{now:%Y-%m-%d %H:%M}')
    
    >> 2021-08-20 15:13
```
   
### форматирование в Python 3
```python
    print(f"{'Username'}:25}{'Role':20}{'License Type'}")
    print(f"{'-' * 23}{' ' * 2}{'-' * 18}{' ' * 2}{'-' * 15}")
    for user in user_list:
        print(f"{user.username:25}{user.role:20}{user.userLicenseTypeId}")
```
       
### кодировки   
```python
    from os import environ
    environ['NLS_LANG'] = 'RUSSIAN_CIS.CL8MSWIN1251'
    environ['NLS_LANG'] = 'American_America.AL32UTF8'    
```
   
### сохранение в файл
```python
    def save_to_file(file_name, data):
    # дописывает в файл, если он уже существует (mode = 'a'), перезаписывает - mode = 'w'
        with open(file_name, 'a') as f:
            f.write('{0}\n'.format(data))
            # log_file.write('{0}\n'.format(message.encode('cp1251')))     
```   
   
### работа с именованными (keyword) аргументами   
```python
# **kwargs (https://realpython.com/python-kwargs-and-args/)
    def test(**kwargs):
        print kwargs['a']
        print kwargs['b']
    
test(a='asdf', b='zxcv')
>>asdf
>>zxcv
```
   
### progress bar
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
   
### еще пример progressbar 
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
   
### копирование папки с сохранением структуры
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

### проверка XML на соответствие схеме    
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

### работа с итератором
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
    
### разбить словарь на части
```python
from itertools import islice

def chunks(data, size=10000):
    it = iter(data)
    for i in range(0, len(data), size):
        yield {k: data[k] for k in islice(it, size)}
      
# использование:
for item in chunks({i:i for i in range(10)}, 3):
   print(item)
   
```   
    
### кастомный класс ошибки
```python    
    class MyCustomError(Exception):
        def __init__(self, *args):
            if args:
                self.message = args[0]
            else:
                self.message = None

        def __str__(self):
            # для Python 3 - неактуально
            print('calling str')
            if self.message:
                return 'MyCustomError, {0} '.format(self.message)
            else:
                return 'MyCustomError has been raised'

# raise MyCustomError
raise MyCustomError('We have a problem')
```
   
### пример создания dataclass (Python 3.7 and over)
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
   
### сохранение / загрузка json данных 
```python
    import json
    with open(<dump_file_name>, 'w', encoding='utf-8') as outfile:    
        json.dump(<data_dict>, outfile, ensure_ascii=False)   
        
    with open(<dump_file_name>) as json_file:
        data = json.load(json_file)
```
  
### функция-декоратор, для определения времени выполнения функции в секундах
```python
    import time
    def time_of_function(function):
        def wrapped(*args, **kwargs):
            start_time = time.time()
            res = function(*args, **kwargs)
            est_time = time.time() - start_time
            if est_time < 300:
                msg = f"{function.__name__} running: {est_time:.4f} sec."
            else:
                msg = f"{function.__name__} running: more then {est_time/60:.4f} min. ({est_time} sec.)"
            print(msg)
            local_log.debug(msg)
            return res
        return wrapped
        
# использование  
from <module> import time_of_function 

    @time_of_function
    def _foo():
        <....>

    >> foo running: 0.2 sec.        
```
   
 ### список файлов в дирректории c определенным расширением
```python
    import os
    list_of_file = []
    _path = <путь к папке>
    for root, dirs, files in os.walk(_path):
        for file in files:
            if file.endswith('.csv'):
                list_of_file.append(os.path.join(root, file))
                log.debug(u'files: {0}'.format(os.path.join(root, file)))
```
   
      
---
---   

## ArcPy & ArcGIS   
    
### работа с тулбоксом
```python    
    # При обновлении набора инструментов Python происходит обновление только самого файла 
    # набора инструментов — импортированные в его состав модули не затрагиваются. 
    # Для перезагрузки модуля из набора инструментов Python используйте функцию importlib модуля reload, 
    # которая может быть временно добавлена.
    import yourmodule
    import importlib
    importlib.reload(yourmodule)  # force reload of the module 
```
    
### нотации: математическая, геодезическая    
- X - Долгота (на восток)   
- Y - Широта (на север)   
   
### создание полей в feature class или table   
```python
    fields = [
        ("LONG", "LONG", "", "", "", "Длинное целое", "NULLABLE", "NON_REQUIRED", ""), 
        ("SHORT", "SHORT", "", "", "", "Короткое целое", "NULLABLE", "NON_REQUIRED", ""),
        ("TEXT", "TEXT", "", "", 64, "Текст", "NULLABLE", "NON_REQUIRED", ""),
        ("DOUBLE", "DOUBLE", 15, 8, "", "С плавающей точкой", "NULLABLE", "NON_REQUIRED", ""),
        ("DATE", "DATE", "", "", "", "Дата", "NULLABLE", "NON_REQUIRED", "")
    ]
    for field in fields:
        arcpy.AddField_management(*(<feature class/table>,) + field)    
        
    # еще один способ добавления полей (https://pro.arcgis.com/ru/pro-app/latest/tool-reference/data-management/add-fields.htm)
    arcpy.management.AddFields(
            <feature class/table>, 
            [
                ['school_name', 'TEXT', 'Name', 255, 'Hello world', ''], 
                ['street_number', 'LONG', 'Street Number', None, 35, 'StreetNumDomain'],
                ['year_start', 'DATE', 'Year Start', None, '2017-08-09 16:05:07', '']
            ])        
```   
### блок исключения    
```python
    try:
        <arcpy operation or tools>
    except (arcpy.ExecuteError, RuntimeError) as err:
        self._error_message(f"arcpy error: {arcpy.GetMessages(2)}")
        self._error_message(str(err))
```
   
### работа с курсорами (Cursor)   
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
   
### удаление записи курсором
```python
    with arcpy.da.UpdateCursor(<feature_class>, ["OID@"], where_clause=<condition>) as update_cursor:
        for row in update_cursor:
            update_cursor.deleteRow()
```
   
### проверить есть ли записи в курсоре
```python
    if any(arcpy.da.SearchCursor(FeatureClass, fieldnames, where_clause)):
        есть
    else:
        нет
```    

### узнать количество записей в курсоре   
```python
# способ 1:
    with arcpy.da.SearchCursor(FeatureClass, fieldnames, where_clause) as srcToday:
        count = sum(1 for row in srcToday)
# способ 2:
    featureList = [row[0] for row in arcpy.da.SearchCursor(FeatureClass, fieldnames, where_clause) ]
    count = len(featureList)
```
    
### работа с Редактором (Editor)
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
    
### получение JSON в ArcMap
```python 
    import arcpy
    lyr = 'lyr'
    arcpy.MakeFeatureLayer_management(<Название класса>, lyr)
    arcpy.FeatureSet(lyr).JSON
```
   
### список полей в таблице raw_table
```python
    exclude_flds = ['OBJECTID']
    raw_table_flds = [fld.name for fld in arcpy.ListFields(raw_table) if fld.name not in exclude_flds]
    print (raw_table_flds)
```

### расчет в поле автоинкримента (ArcMap)   
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
       
### расчет в поле GUID (ArcMap)    
```python
def calc():
    from uuid import uuid4
    return u'{{{0}}}'.format(uuid4()).upper()
```
### случайное значение из диапазона (ArcMap)
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
   
### сдвиг точки на угол и расстояние FieldCalculator (shiftXYCoordinates(!SHAPE!, !Angle! ,5000))
```python
def shiftXYCoordinates(shape,angle,distance):
    point = shape.getPart(0)
    point.Y += distance * math.cos(math.radians(angle))
    point.X += distance * math.sin(math.radians(angle))
    return point     
```

### сдвиг точки в координаты из полей (X, Y). FieldCalculator на поле SHAPE(move_xy(!SHAPE!, !X! ,!Y!))
```python
def move_xy(shape,x,y):
    point = shape.getPart(0)
    point.Y = y
    point.X = x
    return point     
```
   
### определение расстояний между точками
```python
    import arcpy
    sr = arcpy.SpatialReference(102100)   
    p1 = arcpy.PointGeometry(arcpy.Point(11514992.9328,6642257.7652),sr)
    p2 = arcpy.PointGeometry(arcpy.Point(11512492.9328,6639757.7652),sr)
    a1,d1 = p1.angleAndDistanceTo(p2,'GEODESIC') # PLANAR
    a2,d2 = p2.angleAndDistanceTo(p1,'GEODESIC') # PLANAR
    print("Distance = {:8.3f} meters, Bearing1->2 = {:9.5f} degrees".format(d1,a1))
    print("Distance = {:8.3f} meters, Bearing2->1 = {:9.5f} degrees".format(d2,a2))
    >> Distance = 2221.212 meters, Bearing1->2 = -134.91526 degrees
    >> Distance = 2221.212 meters, Bearing2->1 =  45.06726 degrees   
```

### Вывод объектов геометрии
```python
    # Выходной объект геометрии можно создать, задав в качестве выхода инструмента геообработки пустой объект геометрии. 
    # При запуске инструмента с назначением пустого объекта геометрии инструмент возвращает список объектов геометрии. 
    # В следующем примере инструмент Копировать объекты используется, чтобы вернуть список объектов геометрии, 
    # которые можно затем зациклить, чтобы накопить общую длину всех объектов
    
    import arcpy
    # Run the CopyFeatures tool, setting the output to a geometry object. Geometries is returned as a list of geometry objects.
    geometries = arcpy.CopyFeatures_management('c:/temp/outlines.shp', arcpy.Geometry())
    # Walk through each geometry, totaling the length
    length = sum([g.length for g in geometries])
    print('Total length: {}'.format(length)) 
```
      
### Транслитерация
```python
def trans(text):
    """
    Функция транслитерирует текст с русского на английский в соответсвии с правилами:
    https://transliteration.pro/zagranpasport
    переделано “й”, “ю” и “я”, на соответственно “y”, “yu” и “ya”
    :param text: текст на русском
    :return: русский текст транслитерацией а английский
    """
    symbols = (
        "абвгдеёжзийклмнопрстуфхцчшщъыьэюяАБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ",
        (
            *list('abvgdee'), 'zh', *list('ziyklmnoprstuf'), 'kh', 'ts', 'ch', 'sh', 'shch', '', 'y', '', 'e', 'yu', 'ya',
            *list('ABVGDEE'), 'ZH', *list('ZIYKLMNOPRSTUF'), 'Kh', 'Ts', 'Ch', 'Sh', 'Shch', *list('_Y_E'), 'Yu', 'Ya'
        )
    )
    coding_dict = {source: dest for source, dest in zip(*symbols)}
    ret = ''
    if text is not None:
        for letter in text:
            if letter in coding_dict.keys():
                ret += coding_dict[letter]
            else:
                ret += letter
    else:
        ret = None
    return ret      
```    
      
---   

# PANDAS

### класс ArcGIS в датафрейм
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
    
### использование arcpy.da.InsertCursor вместо arcpy.da.NumPyArrayToTable    
```python
# https://gis.stackexchange.com/questions/221660/numpyarraytotable-runtimeerror-unsupported-time-units-use-m8us   
# create a feature class
#...
# add fields from df.columns
#...

    rows_to_write = [tuple(r[1:]) for r in df.itertuples()] 
    with arcpy.da.InsertCursor(out_fc,df.columns) as ins_cur:
        for row in rows_to_write:
            ins_cur.insertRow(row)
```
    
### выбор строк, которые соответствуют нескольким условиям
```python
df.loc[((df['col1'] == 'A') & (df['col2' ] == 'G'))]
```   
   
### выбор строк, которые соответствуют одному из нескольких условий
```python
df.loc[((df['col1'] > 10) | (df['col2' ] < 8))]
```

# POSTGRESQL 
    
###  создание БД и пользователя   
В Postgresql есть приложение psql (командная строка). Но тут стоит учесть, что вход в базу осуществляется (по умолчанию) 
с тем же пользователем, что и тот, под которым вы зарегистрированы в системе. 
Postgresql создаёт при установке пользователя postgres (системного). 
Именно под его учётной записью необходимо выполнять все действия. 
Итак, сначала становимся пользователем postgres:     
> sudo su postgres     
    
и запускаем под ним psql. Далее выведется приглашение командной строки postgres. 
Стоит упомянуть, что в Postgresql пользователь postgres - это что-то вроде суперпользователя, т.е. он имеет доступ ко всем базам 
и по умолчанию все базы создаются от него. 
Также есть небольшой набор команд для администрирования, например, \l - вывести список доступных баз данных. 
Чтобы создать базу данных необходимо написать стандартную команду SQL:      
> CREATE DATABASE test_db;     
    
, например. Чтобы создать пользователя воспользуйтесь командой:
> CREATE USER test_user WITH password 'qwerty';     
    
Но на данную базу данных у пользователя не будет прав. Чтобы создать базу с владельцем добавьте опциональный параметр **OWNER**:    
> CREATE DATABASE test_database OWNER test_user;    
   
Можно также дать права на базу пользователю командой:    
> GRANT ALL privileges ON DATABASE test_db TO test_user;     
     
Для удаления базы данных можно воспользоваться командой:     
> DROP DATABASE test_db;     
    
    