# Form fields

## Line

    $form = $page->add('Form');
    $form->addField('Line','name');
    $form->addSubmit('Reverse string');
    $form->onSubmit(function($form){
        $string = iconv('utf-8', 'utf-16le', $form->get('name'));
        $string = strrev($string);
        $string = iconv('utf-16be', 'utf-8', $string);
        $form->js()->univ()->alert($string)->execute();
    });

## Password

    $form = $page->add('Form');
    $form->addField('Password','secret');
    $form->addSubmit('Show Password');
    $form->onSubmit(function($form){
        $form->js()->univ()->alert("Your password is: \n".$form->get('secret'))->execute();
    });

## Checkbox

    $form = $page->add('Form');
    $form->addField('Checkbox','is_active');
    $form->addSubmit('Submit');
    $form->onSubmit(function($form){
        $res = "Checkbox is ".(($form->get('is_active'))?'active':'NOT active');
        $form->js()->univ()->alert($res)->execute();
    });

## CheckboxList

    $produsers = array(
        1=>'Mr John',
        2=>'Piter Gabriel',
        3=>'Michail Gershwin',
        4=>'Bread and butter',
        5=>'Alex Green',
        6=>'Benjamin Franklin',
        7=>'Rhino',
    );
    $form = $page->add('Form');
    $form->addField('CheckboxList','producers')->setValueList($produsers);
    $form->addSubmit('Submit');
    $form->onSubmit(function($form) use ($produsers){
        $list = '';
        $ids = explode(',',$form->get('producers'));
        foreach ($ids as $id) {
            $list .= $produsers[$id]."\n";
        }
        if (trim($list) == '') $list = 'nobody';
        $form->js()->univ()->alert("Produsers: \n\n". $list)->execute();
    });

## DatePicker

    $form = $page->add('Form');
    $form->addField('DatePicker','date');
    $form->addSubmit('Submit');
    $form->onSubmit(function($form){
        $form->js()->univ()->alert($form->get('date'))->execute();
    });

## DropDown

    $produsers = array(
        1=>'Mr John',
        2=>'Piter Gabriel',
        3=>'Michail Gershwin',
        4=>'Bread and butter',
        5=>'Alex Green',
        6=>'Benjamin Franklin',
        7=>'Rhino',
    );
    $form = $page->add('Form');
    $form->addField('DropDown','producers')->setValueList($produsers);
    $form->addSubmit('Submit');
    $form->onSubmit(function($form) use ($produsers){
        $form->js()->univ()->alert(
             $produsers[$form->get('producers')]
        )->execute();
    });

## Radio

    $produsers = array(
        1=>'Mr John',
        2=>'Piter Gabriel',
        3=>'Michail Gershwin',
        4=>'Bread and butter',
        5=>'Alex Green',
        6=>'Benjamin Franklin',
        7=>'Rhino',
    );
    $form = $page->add('Form');
    $form->addField('Radio','producers')->setValueList($produsers);
    $form->addSubmit('Submit');
    $form->onSubmit(function($form) use ($produsers){
        $form->js()->univ()->alert(
             $produsers[$form->get('producers')]
        )->execute();
    });

## Slider

    $form   = $page->add('Form');
    $value  = $form->addField('Line','value');
    $slider = $form->addField('Slider','slider');
    $slider->min = 10;
    $slider->max = 100;
    $slider->setLabels('Left','Right');
    $slider->js('change',
        $value->js()->val($slider->js()->val())
    );
    $form->addSubmit('Submit');
    $form->onSubmit(function($form){
        $form->js()->univ()->alert(
             $form->get('slider')
        )->execute();
    });

## Textarea

    $form   = $page->add('Form');
    $form->addField('Text','text');
    $form->addSubmit('Revert Text');
    $form->addButton('Set testing text')->js('click',
        $form->getElement('text')->js()->val('А роза упала на лапу Азора')
    );
    $form->onSubmit(function($form){
        $string = iconv('utf-8', 'utf-16le', $form->get('text'));
        $string = strrev($string);
        $string = iconv('utf-16be', 'utf-8', $string);
        $form->getElement('text')->js()->val($string)->execute();
    });














