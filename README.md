# cot_fileAPI
Модуль загрузки файлов для Cotonti

Модуль на стадии разработки, но можно уже побаловаться...


# Прикрепление файлов к страницам

в файл page.add.tpl
----
вставляем вызов формы: 
```html
<!-- IF {PHP|cot_module_active('fileAPI')} -->	
  {PHP|fileAPI_prepare('page')}
  {PHP.cfg.fileAPI.prepare|fileAPI_form('$this,dnd:1')} 
<!-- ENDIF -->
```
в файл page.edit.tpl
----
```html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
  {PHP|fileAPI_form('area:page,cat:$pag.page_cat,indf:$id,dnd:1')} 
<!-- ENDIF -->	
```
параметр dnd:1 - загрузка с поддержкой Drag&Drop. dnd:0 - без поддержки..

Файл page.tpl
------
Для вывода прикрепленных файлов к странице вставляем:

Вывод всех файлов(изображение и файлы):

```html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
  {PHP|fileAPI_files('area:page, cat:$c, indf:$id, type:all' ,'thumb')} 
<!-- ENDIF -->
```
Вывод изображений:

```html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
  {PHP|fileAPI_files('area:page, cat:$c, indf:$id, type:image' ,'thumb')} 
<!-- ENDIF -->
```
Вывод файлов:

```html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
  {PHP|fileAPI_files('area:page, cat:$c, indf:$id, type:file' ,'thumb')} 
<!-- ENDIF -->
```

Файл page.list.tpl:
-----
Вывод файлов к страницам в списке страниц.

````html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
  {LIST_ROW_ID|fileAPI_files('loop:1, area:page, indf:$this, type:all','thumb')} 
<!-- ENDIF -->
````
в блок <!-- BEGIN: LIST_ROW --> ... <!-- END: LIST_ROW -->
параметр loop:1 указывает на режим с минимальным кол. запросов к базе.

Если не поставить значение в 1, то каждый вывод к странице будет тянуть 1 обращение к базе MySQL.


# Прикрепление файлов к постам на форуме

Вставить вызов формы в файлы:

forums.newtopic.tpl
-------
вставляем в районе тега {FORUMS_NEWTOPIC_TEXT}

````html
<!-- IF {PHP|cot_module_active('fileAPI')} -->	
	{PHP|fileAPI_prepare('forum')}
	{PHP.cfg.fileAPI.prepare|fileAPI_form('$this,dnd:1')} 
<!-- ENDIF -->	
````

forums.posts.tpl
-------
вставляем в районе тега {FORUMS_POSTS_NEWPOST_TEXT} в блоке <!-- BEGIN: FORUMS_POSTS_NEWPOST --> ... <!-- END: FORUMS_POSTS_NEWPOST -->

````html
<!-- IF {PHP|cot_module_active('fileAPI')} -->	
	{PHP|fileAPI_prepare('forum')}
	{PHP.cfg.fileAPI.prepare|fileAPI_form('$this,dnd:1')} 
<!-- ENDIF -->		
````
вставляем в районе тега {FORUMS_POSTS_ROW_TEXT} в блоке <!-- BEGIN: FORUMS_POSTS_ROW --> ... <!-- END: FORUMS_POSTS_ROW -->

````html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
	{FORUMS_POSTS_ROW_ID|fileAPI_files('loop:1,area:forum, cat:$s, indf:$this, type:all','thumb')} 
<!-- ENDIF -->	
````

forums.editpost.tpl
-------
вставляем в районе тега {FORUMS_EDITPOST_TEXT} в блоке <!-- BEGIN: FORUMS_EDITPOST_FIRSTPOST --> ... <!-- END: FORUMS_EDITPOST_FIRSTPOST -->


````html
<!-- IF {PHP|cot_module_active('fileAPI')} -->
	{PHP|fileAPI_form('area:forum,cat:$s,indf:$p,dnd:1')} 
<!-- ENDIF -->		
````

Пока все..
Следите за обновлениями, будет много вкусного ;)
