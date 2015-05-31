Yii2 FileAPI widget.
==================
This widget is a Yii 2 wrapper of [FileAPI](https://github.com/RubaXa/jquery.fileapi) plugin.

this is an adapt for sina app engine

this is based on https://github.com/vova07/yii2-fileapi-widget

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist "postor/yii2-fileapi-sae" "*"
```

or add

```
"postor/yii2-fileapi-sae": "*"
```

to the require section of your `composer.json` file.

Usage:
------

```php
// MyController.php

use postor\fileapi\actions\UploadAction as FileAPIUpload;
...

public function actions()
{
    return [
        'fileapi-upload' => [
            'class' => FileAPIUpload::className(),
            'path' => 'saestor://upload/temp'
        ]
    ];
}
```

```php
// MyModel.php

use postor\fileapi\behaviors\UploadBehavior;
...

public function behaviors()
{
    return [
        'uploadBehavior' => [
            'class' => UploadBehavior::className(),
            'attributes' => [
                'preview_url' => [
                    'path' => 'saestor://upload/temp',
                    'tempPath' => 'saestor://upload/category',
                    'url' => $saeStorage->getUrl('upload','category'),
                ],
            ]
        ]
    ];
}
```

```php
// _form.php

use postor\fileapi\Widget as FileAPI;
...

echo $form->field($model, 'preview_url')->widget(
    FileAPI::className(),
    [
        'settings' => [
            'url' => ['/controller/fileapi-upload']
        ]
    ]
);
```

demo project: http://yii2postor.sinaapp.com/web/index.php?r=admin%2Fcategory%2Fupdate&id=2
