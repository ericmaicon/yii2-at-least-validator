# AtLeastValidator - Yii 2

## Usage


```php
namespace app\models;

...
use slinstj\yii2-validators\AtLeastValidator;

class MyModel extends Model
{
    public $name;
    public $email;
    public $phone;

    public function rules()
    {
        return [
            [['name', 'email'], 'required'],
            [['phone', 'email'], AtLeastValidator::className()],
            // ['name', AtLeastValidator::className(), 'min' => 2, 'in' ['name', 'email, 'phone']] *** using parameters,
            ['email', 'email'],
        ];
    }
}
```

## Examples

In the following example, the `attr1` and `attr2` attributes will
be verified. If none of them are filled `attr1` will receive an error:

```php
     // in rules()
     return [
         ['attr1', AtLeastValidator::className(), 'in' => ['attr1', 'attr2']],
     ];
```

Here, the `attr1`, `attr2` and `attr3` attributes will
be verified. If at least 2 (`min`) of them are not filled, `attr1` will
receive an error:

```php
     // in rules()
     return [
         ['attr1', AtLeastValidator::className(), 'min' => 2, 'in' => ['attr1', 'attr2', 'attr3']],
     ];
```
### Showing errors in summary

If you want to show errors in a summary instead in the own attributes, you can do this:

```php
     // in the rules()
     // please note the exclamation mark. It will avoid the pk attribute to be massively assigned.
     return [
         ['!id', AtLeastValidator::className(), 'in' => ['attr1', 'attr2', 'attr3']], // where `id` is the pk
     ];

     // in the view:
     ...
     echo yii\helpers\Html::errorSummary($model, ['class' => ['text-danger']]);
     // OR, to show only `id` errors:
     echo yii\helpers\Html::error($model, 'id', ['class' => ['text-danger']]);
```
